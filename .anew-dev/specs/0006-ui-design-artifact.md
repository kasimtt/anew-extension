# Spec 0006 — UI spec'lerinde zorunlu tasarım artifact'i (mini)

- Status: In progress
- Mode: lite (ANEW fork development)
- Plan: `.anew-dev/plans/0006-plan.md`
- Self-critique: done (G-1…G-6 aşağıya işlendi)
- Revised (R-08): PB-2 — çekirdekte bugün zaten 11 "Claude" geçişi var; kriter "yeni geçiş
  eklemez" olarak düzeltildi (plan R-2) — approved by kasimislamtatli, 2026-11-12
- Source: sohbet isteği, kasimislamtatli, 2026-11-12 (fork kurulum oturumu; takip sistemi anahtarı yok)
- Design: none — no user interface (bu spec yalnızca şablon metnini ve `doctor`'ı değiştirir)
- Supersedes: — (şablonda bu davranışı tanımlayan shipped spec yok)
- Sensitive area: SA-1, SA-2 (`.anew-dev/FORK.md`)

## Intent
Şablonu kullanan iç ekipler UI işlerinde bugün yalnızca metinle anlaşıyor. Tasarım bağlantısı
isteğe bağlı ve analist ekran çizmiyor ("Never invent visuals"), bu yüzden ekran düzeni ilk kez
BUILD'de görülüyor ve yanlış anlamalar geç yakalanıyor. Bu değişiklikle UI içeren her spec için
analist, analize dayanarak kabul kriterlerinin dokunduğu bütün ekranları kapsayan bir tasarım
artifact'i çizer. Spec bu artifact'in adresini taşır ve spec ile tasarımın **ikisi birden**
onaylanmadan `Approved` olmaz. Clarify kararları: 2026-11-12, 7 önerinin hepsi kabul edildi.

## Changed behavior
- [ ] CB-1 — **Kapsam ve tarafsız kural.** UI spec'lerinde (`specs/TEMPLATE.md` "User experience"
  bölümü `none — no user interface` değil) ve UI değiştiren mini-spec'lerde, `prompts/spec.md` ve
  `prompts/clarify.md` analistten analize dayanarak bir tasarım artifact'i çizmesini ister.
  "Never invent visuals" kuralı bu durumda "tasarımı çiz, insan onaylasın" kuralıyla değiştirilir.
  Çekirdek metin aracı adlandırmaz: "kalıcı adresi olan, sürümlenen bir tasarım artifact'i".
  `specs/TEMPLATE-mini.md` dosyasındaki `Design:` alanı UI değişikliği için zorunlu olur.
- [ ] CB-2 — **Kapsama ve referans.** Artifact, User experience'ta listelenen her
  **ekran × durum** (empty, loading, error, success, no permission) için bir artboard içerir. Her
  artboard hizmet ettiği AC numaralarıyla etiketlenir. Spec'in `Design:` satırı artifact adresini
  ve onaylanan sürümün etiketini taşır. Araç kalıcı bir sürüm kimliği vermiyorsa onaylanan
  tasarımın tarihli bir dışa aktarımı gösterilir. Şablonlar ve `prompts/spec.md` bunu söyler.
- [ ] CB-3 — **Onay kapısı.** `workflows/segments.md` (ANALYZE), `workflows/feature-development.md`
  ve `workflows/change-request.md` (MINI-SPEC) şunu söyler: UI spec'inde tasarım onayı, spec
  onayından **önce** gelen ayrı bir kapı mesajıdır. Koşulu, artifact'in onaylayan kişi, reviewer
  ve QA ile paylaşılmış olmasıdır. Onay `Design approved by / on: <ad>, <YYYY-MM-DD>` satırıyla
  kaydedilir. `Status: Approved` ancak iki onay da kayıtlı olduğunda yazılır. Onaydan sonraki
  her tasarım değişikliği spec değişikliğidir (R-08). `docs/commands.md` yeni kapıyı anlatır.
- [ ] CB-4 — **Adapter'lar.** Claude Code adapter'ı (`adapters/claude-code/`) aracı Claude Design
  artifact'i ("Design" tipi) olarak adlandırır ve onayda bir yayın etiketi
  (`spec <NNNN> — approved`) verilmesini ister. Copilot, Cursor ve Codex adapter'ları aynı kuralı
  araç adı vermeden taşır. `doctor`'ın adapter parity kontrolü `ok` kalır.
- [ ] CB-5 — **`doctor` denetimi.** `specs/active/` altında ya da yeni bir ship'te bulunan, User
  experience'ı `none — no user interface` olmayan ve durumu `Approved`, `In progress` ya da
  `Shipped` olan bir spec'te `Design:` adresi ya da `Design approved by / on:` satırının adı veya
  tarihi boşsa, `doctor` yerelde WARN, `--strict` altında FAIL verir. Mesaj spec numarasını ve
  eksik alanı adlandırır. Mini-spec'lerde UI değişikliği metinden çıkarılamadığı için (G-1),
  yalnızca dolu bir `Design:` alanı `Design approved by / on:` satırını zorunlu kılar; boş
  `Design:` alanını reviewer denetler.
- [ ] CB-6 — **Kanıt testleri.** `scripts/selftest` CB-5'in her yönünü doğrular: eksik adres,
  eksik onay adı veya tarihi, `--strict` altında FAIL, UI'sız spec'in geçmesi, eksiksiz spec'in
  geçmesi, `Draft` durumunun denetlenmemesi, mini-spec kuralı. Toplam test sayısı 281'den artar
  ve hiçbir eski test silinmez ya da zayıflatılmaz.
- [ ] CB-7 — **UI kanıtı.** `docs/testing.md` "Evidence for UI criteria" bölümü, VERIFY ekran
  görüntülerinin onaylanan tasarım sürümünün artboard'larıyla, ekran × durum eşleşmesiyle
  karşılaştırıldığını söyler.

## Preserved behavior
- [ ] PB-1 — **UI'sız akış değişmez.** User experience'ı `none — no user interface` olan bir spec
  için tasarım kapısı sorulmaz, `doctor` yeni bir uyarı vermez ve mevcut 281 selftest geçmeye
  devam eder.
- [ ] PB-2 — **Çekirdek araçtan bağımsız kalır.** `AGENTS.md`, `workflows/`, `prompts/`, `specs/`
  şablonları, `docs/` ve `scripts/` dosyalarına bu değişiklik yeni bir "Claude" geçişi eklemez
  (taban commit'e göre diff; mevcut geçişlere dokunulmaz). `AGENTS.md` invariant blok
  harfi harfine aynı kalır ve dosya ≤ 40 satırdır.
- [ ] PB-3 — **Protokol ve eski kayıtlar.** Mevcut `Status:` değerleri ile `Approved by / on:`
  ve `Source:` etiketleri değişmez. `specs/done/` altındaki eski ship'ler (bu kuraldan önce
  shipped olanlar) için `doctor` yeni bir WARN ya da FAIL vermez: kural yalnızca aktif spec'lere
  ve yeni ship'lere uygulanır.

## Out of scope
- Tasarım sistemleri (renk, tipografi, bileşen kütüphanesi) ve görsel kalite ölçütleri.
- Ekran görüntüsü yakalama mekanizmasının kendisi (`docs/testing.md`'deki capture kuralı aynen kalır).
- `.anew-dev/` kayıtları için `doctor` taraması (`doctor` bu klasörü taramaz).
- B-8 (flaky selftest) ve şablonun sürüm ya da CHANGELOG politikası. CHANGELOG girdisi bu işin
  parçasıdır, ama sürüm numarası kararı ship kapısında verilir.
- **Varsayım (onaylayan teyit eder):** Şirket politikası, iç ekran tasarımlarının claude.ai'da
  paylaşılmış artifact olarak tutulmasına izin veriyor.

## Self-critique (G-n)
- **G-1:** Mini-spec'te UI değişikliği metinden çıkarılamıyor. Bu yüzden `doctor` yalnızca dolu
  `Design:` alanı için onay ister, boş alanı reviewer denetler (CB-5).
- **G-2:** Artifact'in kalıcı sürüm kimliği doğrulanmadı. PLAN bunu doğrular; doğrulanamazsa
  tarihli dışa aktarım kullanılır (CB-2).
- **G-3:** Şablonu yükselten ekiplerin eski ship'leri kırılmamalı (PB-3).
- **G-4:** Artifact metni de doküman dilinde yazılır (`AGENTS.md`, Language); alan etiketleri
  İngilizce kalır.
- **G-5:** Tasarımı ve spec'i aynı kişi onaylayabilir; iki kayıt ayrı tutulur.
- **G-6:** Boyut: 7 CB + 3 PB = 10 kriter, `prompts/spec.md` SIZE sınırının üst ucu. Bölme
  seçeneği: 0006 (kural ve metin: CB-1…4, CB-7) ile 0007 (`doctor` ve selftest: CB-5, CB-6).
  Önerim tek spec olarak kalması; bölünürse kural bir süre denetimsiz yayınlanmış olur.

## Definition of Done
- [ ] Yeşil: `./scripts/doctor --strict` 0 fail **ve** `./scripts/selftest` 0 failed (`.anew-dev/FORK.md`, Yeşilin tanımı)
- [ ] Independent review done; real findings fixed, noise rejected with written rationale, deferred ones in `.anew-dev/backlog.md`
- [ ] Criterion ↔ evidence table complete for CB-* **and** PB-*; her kriter kasıtlı bir kırılmayla kırmızıya düşürülerek kanıtlanır (hassas alan)
- [ ] Spec moved to `.anew-dev/done/` (immutable there)
