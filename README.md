## Git Senaryo Egzersizi - Ödev 1.3 

**1. Yanlış dala commit atıp doğru dala taşıma (Cherry-pick & Reset):**
```bash
git checkout dogru-dal
git cherry-pick <yanlis-commit-hash>
git checkout yanlis-dal
git reset --hard HEAD~1
git rebase -i HEAD~3
# Açılan editörde ilk commit 'pick' bırakıldı, diğerleri 'squash' (s) olarak işaretlenip kaydedildi.
# .env dosyası .gitignore'a eklendi
git rm --cached .env
git commit -m "fix: .env dosyası takipten çıkarıldı ve geçmişten temizlendi"
git add .
git commit -m "fix: merge conflict elle cozuldu"
git bisect start
git bisect bad                 # Mevcut durum hatalı
git bisect good <eski-hash>    # Çalışan eski bir commit
# Git'in yönlendirmesine göre 'git bisect good' veya 'git bisect bad' ile test edildi.
git bisect reset               # İşlem tamamlanınca iptal edildi
