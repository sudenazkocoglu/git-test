# Git Test Ödevi (Ödev 1.3)

Bu repo; Git versiyon kontrol sisteminin gelişmiş özelliklerini (Merge Conflict, Cherry-pick, Reset, Rebase Squash, Ignore/Temizlik ve Bisect) uygulamalı olarak test etmek ve kanıtlamak amacıyla oluşturulmuştur.

---

## 1. Merge Conflict (Çakışma) Senaryosu
* **Durum:** Kanıtlı ve geçmişte commit kayıtlarıyla sabittir.
* **Açıklama:** İki farklı dalda (`main` ve `dal-2`) aynı dosya üzerinde eşzamanlı değişiklikler yapılarak çakışma (conflict) üretilmiş, ardından manuel olarak çözülüp `merge` edilmiştir.

## Uygulanan Komutlar:
```bash
# Çakışma yaratılan dalların birleştirilmesi sırasında oluşan conflict'in çözümü:
git status
# Çakışmalı dosya manuel düzenlendikten sonra:
git add <dosya_adi>
git commit -m "fix: merge conflict elle cozuldu"

2. Cherry-pick ve Reset Senaryosu
Açıklama: Yanlış dala atılan bir commit'in cherry-pick ile doğru dala alınması ve eski daldaki fazlalık commit'in reset ile temizlenmesi sürecidir.

Uygulanan Komutlar:
# Doğru dala (main) geçiş ve commit'i çekme
git checkout main
git cherry-pick 8d2b4ad

# Test dalına dönüp oradaki fazla commit'i temizleme
git checkout test-cherry-pick
git reset --hard HEAD~1

Gerçek İşlem Kanıtı (Git Log):
* 5fc3cd2 (HEAD -> main) feat: cherry-pick edilecek ornek commit
* 54002d2 (origin/main) docs: git-test README senaryo basliklari ve duzenli kod bloklariyla guncellendi
* 4280404 Update title and section heading in README.md
* d1f3577 docs: odev 1.3 senaryo komutlari not edildi
*   4b5f049 conflict cozuldu ve README birlestirildi
|\  
| * 9bdf1c3 Create README.md
* | 5b980e6 docs: 1.3 ödevi için README eklendi
* | a59562c fix: merge conflict elle cozuldu
|/  
* | f5faee8 (dal-2) fix: dal-2 tarafindan guncellendi
* | ae935c7 fix: main tarafindan guncellendi

3. Rebase ve Squash Senaryosu
Açıklama: Git geçmişini (history) düzenlemek ve birden fazla ardışık commit'i tek bir anlamlı commit altında birleştirmek (squash) için interaktif rebase kullanılmıştır.

Uygulanan Komutlar:
# Son 3 commit üzerinde interaktif rebase başlatma
git rebase -i HEAD~3
# Açılan editörde ilk commit 'pick', diğerleri 'squash' (s) olarak işaretlenip kaydedilmiştir.

Gerçek İşlem Kanıtı (Git Log):
* c031baa (HEAD -> test-squash) feat: 3 taslak commit squash ile birlestirildi
* b902aec (origin/main, main) docs: odev 1.3 - cherry-pick senaryosu gercek log kaniti ile guncellendi
* 035c7db feat: cherry-pick edilecek ornek commit
* 6972b7a Fix formatting and update command sections in README
* 54002d2 docs: git-test README senaryo basliklari ve duzenli kod bloklariyla guncellendi

4. .env Temizliği Senaryosu
Açıklama: Hassas bilgilerin (.env) versiyon kontrol sistemine yanlışlıkla dahil edilmesini önlemek ve .gitignore kuralını uygulamak amacıyla yapılan temizlik adımıdır.

Uygulanan Komutlar:
# .env dosyasının takipten çıkarılması
git rm --cached .env
git commit -m "fix: .env dosyasi takipten cikarildi"

Gerçek İşlem Kanıtı (Git Log):
* 033237f (HEAD -> main) fix: .env dosyasi git takibinden cikarildi ve temizlendi
* b85e272 feat: projeye env dosyasi eklendi (yanlislikla)
* 847e016 (origin/main) docs: odev 1.3 - squash senaryosu gercek log kaniti ile guncellendi
* b902aec docs: odev 1.3 - cherry-pick senaryosu gercek log kaniti ile guncellendi
* 035c7db feat: cherry-pick edilecek ornek commit

5. Git Bisect Senaryosu
Açıklama: Kod tabanında hatanın (bug) ilk ortaya çıktığı commit'i ikili arama (binary search) algoritmasıyla bulmak için git bisect aracı kullanılmıştır.

Gerçek İşlem Kanıtı (Terminal Çıktısı):
$git bisect start$ git bisect bad

$ git bisect good 54002d2

Bisecting: 1 revision left to test after this (roughly 1 step)
[035c7db6d2214d42fd807977e16d89d581ee3d5c] feat: cherry-pick edilecek ornek commit

$ git bisect bad
035c7db6d2214d42fd807977e16d89d581ee3d5c is the first bad commit
commit 035c7db6d2214d42fd807977e16d89d581ee3d5c
Author: Sudenaz Kocoglu

$ git bisect reset
Previous HEAD position was 035c7db feat: cherry-pick edilecek ornek commit
Switched to branch 'main'

