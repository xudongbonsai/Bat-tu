# 🚀 Hướng Dẫn Deploy Minh Kính Đài Lên GitHub Pages

## 📋 Checklist Trước Khi Deploy

- [ ] Đã có tài khoản GitHub
- [ ] Đã cài đặt Git trên máy tính
- [ ] Đã cài đặt Node.js (version 16+)
- [ ] Đã download và giải nén source code

## 🔧 Bước 1: Chuẩn Bị Repository

### 1.1 Tạo Repository Mới
1. Đăng nhập vào [GitHub.com](https://github.com)
2. Click nút **"New"** hoặc **"+"** → **"New repository"**
3. Điền thông tin:
   - **Repository name**: `minh-kinh-dai` (hoặc tên bạn muốn)
   - **Description**: `Hệ thống Bát Tự AI tiên tiến`
   - **Visibility**: Chọn **Public** (bắt buộc cho GitHub Pages miễn phí)
   - **KHÔNG** tích vào "Add a README file"
4. Click **"Create repository"**

### 1.2 Clone Repository Về Máy
```bash
# Thay [username] và [repository-name] bằng thông tin của bạn
git clone https://github.com/[username]/[repository-name].git
cd [repository-name]
```

## 📁 Bước 2: Upload Source Code

### 2.1 Copy Files
Copy toàn bộ nội dung từ thư mục `minh-kinh-dai-github-pages` vào thư mục repository vừa clone.

### 2.2 Cập Nhật Cấu Hình
Mở file `vite.config.js` và thay đổi dòng:
```javascript
base: '/minh-kinh-dai/', // Thay bằng tên repository của bạn
```

Thành:
```javascript
base: '/[tên-repository-của-bạn]/',
```

### 2.3 Commit và Push
```bash
# Add tất cả files
git add .

# Commit với message
git commit -m "Initial commit: Minh Kinh Dai production ready"

# Push lên GitHub
git push origin main
```

## ⚙️ Bước 3: Cấu Hình GitHub Pages

### 3.1 Enable GitHub Pages
1. Vào repository trên GitHub
2. Click tab **"Settings"**
3. Scroll xuống phần **"Pages"** (menu bên trái)
4. Trong **"Source"**, chọn **"GitHub Actions"**

### 3.2 Kiểm Tra Workflow
1. Click tab **"Actions"**
2. Bạn sẽ thấy workflow **"Deploy to GitHub Pages"** đang chạy
3. Đợi cho đến khi có dấu ✅ xanh (thường mất 2-5 phút)

## 🌐 Bước 4: Truy Cập Website

Sau khi deploy thành công, website sẽ có URL:
```
https://[username].github.io/[repository-name]/
```

Ví dụ: `https://johndoe.github.io/minh-kinh-dai/`

## 🧪 Bước 5: Test Local (Tùy Chọn)

Để test trên máy local trước khi deploy:

```bash
# Cài đặt dependencies
npm install

# Chạy development server
npm run dev
# Website sẽ mở tại http://localhost:3000

# Build production để test
npm run build
npm run preview
# Website sẽ mở tại http://localhost:4173
```

## 🔧 Troubleshooting

### Lỗi Build Failed
**Triệu chứng**: GitHub Actions báo lỗi, có dấu ❌ đỏ

**Giải pháp**:
1. Kiểm tra logs trong tab **Actions**
2. Thường do thiếu dependencies hoặc syntax error
3. Fix lỗi và push lại:
```bash
git add .
git commit -m "Fix build errors"
git push origin main
```

### Website Không Load
**Triệu chứng**: Truy cập URL nhưng hiển thị 404 hoặc blank page

**Giải pháp**:
1. Kiểm tra `base` URL trong `vite.config.js`
2. Đảm bảo repository là **Public**
3. Đợi 5-10 phút để GitHub Pages update
4. Clear browser cache (Ctrl+F5)

### CSS/JS Không Load
**Triệu chứng**: Website hiển thị nhưng không có style hoặc tính năng

**Giải pháp**:
1. Kiểm tra browser console (F12) xem có lỗi 404 không
2. Đảm bảo `base` URL đúng trong `vite.config.js`
3. Rebuild và redeploy

### Routing Không Hoạt Động
**Triệu chứng**: Click link bị 404, refresh page bị lỗi

**Giải pháp**:
- App đã sử dụng `HashRouter`, URLs sẽ có dạng `/#/about`
- Đây là normal behavior cho GitHub Pages

## 🎯 Demo Accounts

Để test các tính năng sau khi deploy:

**Admin Account**:
- Email: `admin@minhkinhdat.com`
- Password: `admin123`

**User Account**:
- Email: `user@example.com`
- Password: `user123`

## 📱 Test Checklist

Sau khi deploy thành công, test các tính năng:

- [ ] **Homepage**: Load đúng, responsive
- [ ] **Bazi Analysis**: Form hoạt động, hiển thị kết quả
- [ ] **Login/Register**: Authentication flow
- [ ] **Pricing**: Hiển thị gói dịch vụ
- [ ] **Dashboard**: User dashboard (sau khi login)
- [ ] **Admin**: Admin dashboard (login với admin account)
- [ ] **Mobile**: Test trên điện thoại
- [ ] **Performance**: Tốc độ load trang

## 🔄 Cập Nhật Website

Để cập nhật website sau này:

```bash
# Thay đổi code
# ...

# Commit và push
git add .
git commit -m "Update: [mô tả thay đổi]"
git push origin main

# GitHub Actions sẽ tự động deploy lại
```

## 🎨 Customization

### Thay Đổi Branding
1. **Logo**: Thay file trong `/public/`
2. **Title**: Sửa `index.html` và các page components
3. **Colors**: Cập nhật `tailwind.config.js`
4. **Content**: Chỉnh sửa text trong các components

### Thêm Domain Tùy Chỉnh
1. Mua domain (VD: `minhkinhdat.com`)
2. Tạo file `public/CNAME` với nội dung là domain
3. Cấu hình DNS trỏ về GitHub Pages
4. Cập nhật `base: '/'` trong `vite.config.js`

## 📞 Hỗ Trợ

Nếu gặp vấn đề:

1. **Check GitHub Actions**: Tab Actions để xem logs
2. **Browser Console**: F12 để xem errors
3. **GitHub Issues**: Tạo issue trong repository
4. **Documentation**: Đọc lại README.md

## 🎉 Hoàn Thành!

Chúc mừng! Bạn đã deploy thành công Minh Kính Đài lên GitHub Pages.

**Next Steps**:
1. Share URL với bạn bè để test
2. Setup Google Analytics (nếu cần)
3. Cấu hình payment gateways thật (cho production)
4. Launch marketing campaigns

---

**Happy Coding! 🚀**
