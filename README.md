# Tao file IPA tren Windows de ky bang ESign

Du an mau SwiftUI: viet code tren Windows, build IPA chua ky tren macOS cua GitHub Actions.

## 1. Up source len GitHub

- Tao repository moi tren https://github.com/new, branch `main`.
- Giai nen ZIP va tai len **noi dung** thu muc nay, bao gom `.github/workflows/build-ipa.yml`.
- Neu Windows an thu muc `.github`, hay bat View > Show > Hidden items trong File Explorer.
- Repo public co the su dung GitHub Actions hosted runner theo dieu khoan free hien hanh; repo private co han muc/phat sinh phi tuy tai khoan.

Hoac dung Git trong PowerShell tai thu muc du an:

```powershell
git init
git branch -M main
git add .
git commit -m "Initial iOS app"
git remote add origin https://github.com/USERNAME/REPO.git
git push -u origin main
```

## 2. Build

Vao repository > Actions > Build unsigned iOS IPA > Run workflow.
Neu push vao main, workflow cung se chay tu dong.
Cho job thanh cong > Artifacts > tai DemoIPA-unsigned.zip ve, giai nen de lay DemoIPA-unsigned.ipa.

## 3. Ky bang ESign tren iPhone

- Chuyen DemoIPA-unsigned.ipa qua iPhone (vi du iCloud Drive).
- ESign phai duoc cai va hoat dong; ban can chung chi `.p12` kem mat khau va `.mobileprovision` phu hop voi iPhone va bundle ID.
- ESign > Files > Import > chon IPA > Import to App Library > Apps > Sign > chon chung chi > Sign > Install.
- Tren iOS, co the can bat Developer Mode/chap nhan profile theo loai ky.

Luu y: Chung chi bi thu hoi, profile khong dung UDID/App ID, hoac entitlement khong hop le se khien app khong cai hoac khong mo duoc. Khong nhap mat khau Apple ID vao dich vu ky khong tin cay.

## 4. Chinh sua app

- Giao dien / logic: `DemoIPA/DemoIPAApp.swift`.
- Bundle ID: `project.yml` -> `PRODUCT_BUNDLE_IDENTIFIER` (thay `com.example.demoipa` bang ID rieng).
- Ten hien thi: `INFOPLIST_KEY_CFBundleDisplayName`.
- Muc tieu thap nhat iOS 15: `deploymentTarget`.
- Sau khi sua, commit/push va chay lai workflow.

## 5. Luu y

File .ipa nay la goi **chua ky**, khong the cai truc tiep. ESign chi ky app va cai, khong bien source Swift/HTML/EXE/APK thanh ung dung iOS.

Cau hinh chua duoc kiem chung bang build thuc te tren macOS trong moi truong tao tai lieu nay; neu Xcode/SDK thay doi, can kiem tra log GitHub Actions de dieu chinh.
"# build-ios-app" 
