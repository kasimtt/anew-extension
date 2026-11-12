# Bu repo: ANEW iç fork'u

Bu repo, şirket içi ekiplerin iç yazılım geliştirirken kullanacağı **ANEW yaşam döngüsünün**
geliştirildiği yerdir. Ürün şablonun kendisidir (`AGENTS.md`, `workflows/`, `prompts/`,
`scripts/`, `docs/` şablonları, `adapters/`).

## Karar (R-10, 2026-11-12) — Model A

- **Bu repo bootstrap edilmez.** `AGENTS.md` "NOT CONFIGURED" kalır, `docs/*.md` şablon olarak
  kalır, `scripts/check.conf` yazılmaz. Ekipler bu repo'yu klonlayıp *kendi* projelerinde
  `/bootstrap` çalıştırır.
- Şablondaki her değişiklik upstream'in kendi geliştirme yöntemiyle yapılır: spec ve plan
  `.anew-dev/` altında (`.anew-dev/README.md`). Değişmez kuralların hepsi aynen geçerlidir:
  spec olmadan kod yok, plan onayı, bağımsız review, kanıt.
- Reddedilen seçenekler: B (bu repo'yu normal bootstrap etmek, dağıtılan şablonu kirletir);
  C (ayrı lab ve şablon repo'ları, senkronizasyon yükü).

## Çalışma modu (2026-11-12)

- **lite.** İş `/new-feature "<iş>"` ile başlar ve segmentleri her kapıda onay alarak zincirler.
  Spec'ler `.anew-dev/` altında açılır, `specs/` altında değil. Spec başlığına
  `Mode: lite (ANEW fork development)` yazılır.
- Review ve QA her zaman bağımsız yapılır: salt-okunur reviewer subagent ya da ayrı bir oturum.
- Aynı anda 3 ya da daha fazla kişi `.anew-dev/` işi yürütürse strict'e geçmek yeniden
  değerlendirilir.

## Yeşilin tanımı (2026-11-12)

Bu repo'da `scripts/check.conf` olmadığı için `./scripts/check` çalışacak adım bulamaz.
4. kuraldaki "check green" burada şu demektir:

- `./scripts/doctor --strict` → **0 fail** (şablon durumundaki WARN'lar beklenir) **ve**
- `./scripts/selftest` → **0 failed**.

İkisi de belirli bir commit SHA'sı için yerelde ve CI'da (`.github/workflows/check.yml`)
kanıtlanır. Planın `## Build evidence` bölümüne şöyle yazılır:
`CHECK GREEN (full: doctor --strict + selftest <N>/0) @<sha>`.
Selftest sayısının düşmesi 5. kural (korunan testler) kapsamında bulgudur. Taban değer:
v1.24.1'de **281/0**.

## Hassas alanlar (2026-11-12)

Bir spec bu alanlardan birine dokunuyorsa Constraints bölümünde `Sensitive area: <ad>` yazar.
O zaman lite modda da clarify kapısı sorulur, yalnızca doküman değiştirenler dışında her fix
round yeniden review edilir ve her kriter kasıtlı bir kırılmayla kırmızıya düşürülerek kanıtlanır
(`workflows/README.md`, Modes). `doctor` `.anew-dev/` klasörünü taramaz; bu kuralı reviewer ve
VERIFY denetler. `docs/domain.md` şablon olarak boş kalır.

| Ad | Kapsam | Neden |
|---|---|---|
| **SA-1 Kapı mekanizması** | `scripts/check`, `scripts/doctor`, `scripts/residue`, `.github/workflows/check.yml` | Bir çıkış kodu ya da ayrıştırma hatası (fail-open) bütün ekiplerde kırmızı işi geçirir. |
| **SA-2 Değişmez kurallar ve protokol alanları** | `AGENTS.md` invariant blok, `specs/TEMPLATE*.md`, `specs/plans/TEMPLATE.md`, `Status:` / `Approved by / on:` / `Source:` etiketleri | Kapılar bu alanları okuyarak karar verir; bir etiket değişirse onay kaydı sessizce geçersiz olur. |
| **SA-3 Ajan izinleri ve korumalar** | `adapters/*` izin listeleri ve hook'lar (`protect-shipped.sh`, deny listesi), reviewer agent araç listesi | Reviewer'a yazma yetkisi sızarsa ya da `specs/done` koruması kaybolursa 3. ve 7. kurallar fiilen ortadan kalkar. |

`prompts/`, `workflows/` ve `docs/` şablonlarındaki düz metin değişiklikleri hassas sayılmaz;
onları normal bağımsız review yakalar.

## Önemsiz değişiklikler (2026-11-12)

- Politika **(1): PR + bir reviewer, spec yok.** Yalnızca `workflows/change-request.md`
  triyajının TRIVIAL dediği değişiklikler için geçerlidir: hiçbir kabul kriteri değişmez,
  paylaşılan koda dokunulmaz.
- `trivial/<kısa-ad>` branch'i açılır, tek ve dar bir commit atılır, yeşil zorunludur
  (yukarıdaki tanım). İkinci bir dosya ya da yeni bir test gerekirse yeniden triyaj yapılır.
- SA-1, SA-2 ya da SA-3 kapsamındaki bir dosyaya dokunan değişiklik **hiçbir zaman** önemsiz
  sayılmaz; `/change` ile normal akışa gider.
- Şablonun `docs/git.md` dosyasındaki "Trivial changes" bölümü ekipler için varsayılan olarak
  kalır; bu politika yalnızca bu repo için geçerlidir.

## Upstream kayıtları (2026-11-12)

- Upstream'in `.anew-dev/` kayıtları tutulur: `done/0001`–`0005`, planları ve `backlog.md`
  (B-1…B-7). Bu dosyalar shipped olduğu için değişmez (kural 7).
- Bizim spec numaralarımız **0006**'dan devam eder. Upstream'den alınan düzeltmeler spec
  numarasıyla değil, upstream commit hash'iyle izlenir (`cherry-pick -x`).

## Dil

- Sohbet: Türkçe (`tr`) · Dokümanlar (`.anew-dev/` spec, plan, review ve verify raporları): Türkçe (`tr`).
- Her zaman İngilizce kalanlar: ANEW çekirdek dosyaları ve şablonun kullanıcıya giden metinleri,
  şablon başlıkları ve alan etiketleri, `Status:` değerleri, `Approved by / on:`, `Source:`.

## Git

- `origin` = bu fork'un repo'su; `upstream` = ANEW
  (`engindemirog/ai-native-engineering-workspace`). Upstream'e push kapalı (`DISABLED`).
- Taban: **v1.24.1** (ilk commit'in ağacı `v1.24.1` tag'iyle birebir aynı).
- Upstream'den düzeltme almak: önce `git fetch upstream --tags`, sonra kendi spec'i olan bir
  branch'te `git cherry-pick -x <upstream commit>`. `.anew-dev/` hunk'ları alınmaz.
- Upstream tag'leri yereldedir. `git push --tags` kullanılmaz; kendi sürümlerimizi tag adıyla
  push ederiz.
- Branch ve commit kuralları `docs/git.md` ile aynıdır: default branch'e doğrudan commit yok,
  her iş kendi branch'inde, commit'ler isimli yollarla atılır.
- Fork'un kendi ANEW kararları `docs/decisions/anew/ANEW-F<NNNN>-<slug>.md` olarak, 0001'den
  başlayarak numaralanır. Böylece upstream'in `ANEW-NNNN` sırasıyla çakışmaz (plan 0006, R-1).

## Yerel kurulum (her geliştirici, bir kez)

1. `./scripts/init claude-code` (ya da kendi aracınızın adapter'ı).
2. Adapter çıktısı bu repo'da **commit'lenmez**, çünkü şablonla ekiplere gitmemeli. Bunun için
   `.git/info/exclude` dosyasına `/CLAUDE.md` ve `/.claude/` satırlarını ekleyin.
3. Yerel `CLAUDE.md` dosyasına bu dosyayı işaret eden satırı ekleyin. Böylece ajan
   "NOT CONFIGURED → bootstrap" yönlendirmesine uymaz, bu dosyaya uyar.
