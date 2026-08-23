
# Git Test Ödevi (Ödev 1.3)

Bu repo; Git versiyon kontrol sisteminin gelişmiş özelliklerini (Merge Conflict, Cherry-pick, Reset, Rebase Squash, Ignore/Temizlik ve Bisect) uygulamalı olarak test etmek ve kanıtlamak amacıyla oluşturulmuştur.

---

## 1. Merge Conflict (Çakışma) Senaryosu
* **Durum:** Kanıtlı ve geçmişte commit kayıtlarıyla sabittir.
* **Açıklama:** İki farklı dalda (`main` ve `dal-2`) aynı dosya üzerinde eşzamanlı değişiklikler yapılarak çakışma (conflict) üretilmiş, ardından manuel olarak çözülüp `merge` edilmiştir.
* **Uygulanan Komutlar:**
  ```bash
  # Çakışma yaratılan dalların birleştirilmesi sırasında oluşan conflict'in çözümü:
  git status
  # Çakışmalı dosya manuel düzenlendikten sonra:
  git add <dosya_adi>
  git commit -m "fix: merge conflict elle cozuldu"

## 2. Cherry-pick ve Reset Senaryosu
Açıklama: Yanlış dala atılan bir commit'in cherry-pick ile doğru dala alınması ve eski daldaki fazlalık commit'in reset ile temizlenmesi sürecidir.
Uygulanan Komutlar:
# Doğru dala geçiş ve commit'i çekme
git checkout dogru-dal
git cherry-pick <commit-hash>
# Yanlış dala dönüp son commit'i geri alma
git checkout yanlis-dal
git reset --hard HEAD~1

## 3. Rebase ve Squash Senaryosu
Açıklama: Git geçmişini (history) düzenlemek ve birden fazla ardışık commit'i tek bir anlamlı commit altında birleştirmek (squash) için interaktif rebase kullanılmıştır.
Uygulanan Komutlar:
# Son 3 commit üzerinde interaktif rebase başlatma
git rebase -i HEAD~3
# Açılan editörde ilk commit 'pick', diğerleri 'squash' (s) olarak işaretlenip kaydedilmiştir.

## 4. .env Temizliği Senaryosu
Açıklama: Hassas bilgilerin (.env) versiyon kontrol sistemine yanlışlıkla dahil edilmesini önlemek ve .gitignore kuralını uygulamak amacıyla yapılan temizlik adımıdır.
Uygulanan Komutlar:
# .env dosyasının takipten çıkarılması
git rm --cached .env
git commit -m "fix: .env dosyasi takipten cikarildi"

## 5. Git Bisect Senaryosu
Açıklama: Kod tabanında hatanın (bug) ilk ortaya çıktığı commit'i ikili arama (binary search) algoritmasıyla bulmak için git bisect aracı kullanılmıştır.
Uygulanan Komutlar:
git bisect start
git bisect bad                  # Mevcut hatalı durum
git bisect good <eski-commit>   # Hatanın olmadığı bilinen son çalışan commit
# Git otomatik olarak orta noktadaki commit'i test için seçer. Test sonucuna göre:
git bisect good / bad
# İşlem tamamlandıktan sonra normal duruma dönmek için:
git bisect reset
