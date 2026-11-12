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

## Yerel kurulum (her geliştirici, bir kez)

1. `./scripts/init claude-code` (ya da kendi aracınızın adapter'ı).
2. Adapter çıktısı bu repo'da **commit'lenmez**, çünkü şablonla ekiplere gitmemeli. Bunun için
   `.git/info/exclude` dosyasına `/CLAUDE.md` ve `/.claude/` satırlarını ekleyin.
3. Yerel `CLAUDE.md` dosyasına bu dosyayı işaret eden satırı ekleyin. Böylece ajan
   "NOT CONFIGURED → bootstrap" yönlendirmesine uymaz, bu dosyaya uyar.
