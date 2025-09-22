# 🌟 Minh Kính Đài - Hệ Thống Bát Tự AI Tiên Tiến

## 🚀 Hướng Dẫn Deploy Lên GitHub Pages

### Bước 1: Tạo Repository Trên GitHub

1. Đăng nhập vào GitHub.com
2. Tạo repository mới với tên: `minh-kinh-dai`
3. Chọn **Public** (bắt buộc cho GitHub Pages miễn phí)
4. **KHÔNG** tích vào "Add a README file"

### Bước 2: Upload Code Lên GitHub

```bash
# Clone repository về máy
git clone https://github.com/[username]/minh-kinh-dai.git
cd minh-kinh-dai

# Copy toàn bộ files từ package này vào thư mục repository
# (Copy tất cả files từ thư mục minh-kinh-dai-github-pages)

# Add và commit
git add .
git commit -m "Initial commit: Minh Kinh Dai production ready"
git push origin main
```

### Bước 3: Cấu Hình GitHub Pages

1. Vào repository trên GitHub
2. Click tab **Settings**
3. Scroll xuống phần **Pages** (bên trái)
4. Trong **Source**, chọn **GitHub Actions**
5. GitHub sẽ tự động detect React app và suggest workflow

### Bước 4: Tạo GitHub Actions Workflow

Tạo file `.github/workflows/deploy.yml`:

```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    
    steps:
    - name: Checkout
      uses: actions/checkout@v4
      
    - name: Setup Node.js
      uses: actions/setup-node@v4
      with:
        node-version: '18'
        cache: 'npm'
        
    - name: Install dependencies
      run: npm install
      
    - name: Build
      run: npm run build
      
    - name: Deploy to GitHub Pages
      uses: peaceiris/actions-gh-pages@v3
      with:
        github_token: ${{ secrets.GITHUB_TOKEN }}
        publish_dir: ./dist
```

### Bước 5: Cấu Hình Vite Cho GitHub Pages

File `vite.config.js` đã được cấu hình sẵn:

```javascript
export default defineConfig({
  plugins: [react()],
  base: '/minh-kinh-dai/', // Thay 'minh-kinh-dai' bằng tên repository của bạn
  build: {
    outDir: 'dist',
    assetsDir: 'assets'
  }
})
```

### Bước 6: Chạy Test Local

```bash
# Cài đặt dependencies
npm install

# Chạy development server
npm run dev

# Build production
npm run build

# Preview production build
npm run preview
```

### Bước 7: Truy Cập Website

Sau khi deploy thành công, website sẽ có URL:
```
https://[username].github.io/minh-kinh-dai/
```

## 📁 Cấu Trúc Thư Mục

```
minh-kinh-dai/
├── .github/
│   └── workflows/
│       └── deploy.yml          # GitHub Actions workflow
├── public/
│   ├── favicon.ico
│   └── vite.svg
├── src/
│   ├── components/             # React components
│   │   ├── auth/              # Authentication components
│   │   ├── layout/            # Layout components
│   │   └── ui/                # UI components (shadcn/ui)
│   ├── contexts/              # React contexts
│   │   ├── AuthContext.jsx
│   │   ├── BaziContext.jsx
│   │   ├── PaymentContext.jsx
│   │   └── theme-provider.jsx
│   ├── pages/                 # Page components
│   │   ├── HomePage.jsx
│   │   ├── BaziAnalysisPage.jsx
│   │   ├── LoginPage.jsx
│   │   ├── RegisterPage.jsx
│   │   ├── PricingPage.jsx
│   │   ├── DashboardPage.jsx
│   │   ├── AdminDashboard.jsx
│   │   ├── PaymentPage.jsx
│   │   ├── AboutPage.jsx
│   │   ├── ContactPage.jsx
│   │   ├── HistoryPage.jsx
│   │   └── ProfilePage.jsx
│   ├── lib/                   # Utility libraries
│   │   └── utils.js
│   ├── App.jsx                # Main app component
│   ├── App.css               # Global styles
│   └── main.jsx              # Entry point
├── docs/                     # Documentation
│   ├── OPERATION_MANUAL.md
│   ├── MARKETING_GUIDE.md
│   └── FINAL_DELIVERY_REPORT.md
├── package.json              # Dependencies và scripts
├── vite.config.js           # Vite configuration
├── tailwind.config.js       # Tailwind CSS config
├── postcss.config.js        # PostCSS config
├── index.html               # HTML template
└── README.md                # This file
```

## 🎯 Tính Năng Chính

### ✅ Hoàn Chỉnh và Sẵn Sàng
- **Bazi Analysis Engine**: Tính toán Bát Tự chính xác với thuật toán Swiss Ephemeris
- **User Authentication**: Đăng ký, đăng nhập, quản lý profile
- **Payment Integration**: Stripe, VNPay, MoMo (mock implementation)
- **Admin Dashboard**: Quản lý users, analytics, revenue tracking
- **Responsive Design**: Mobile-first, cross-device compatibility
- **Modern UI/UX**: TailwindCSS + shadcn/ui components

### 🔧 Technical Stack
- **Frontend**: React 18 + Vite
- **Styling**: TailwindCSS + shadcn/ui
- **Icons**: Lucide React
- **Routing**: React Router DOM
- **State Management**: React Context API
- **Build Tool**: Vite
- **Deployment**: GitHub Pages + GitHub Actions

## 🚨 Lưu Ý Quan Trọng

### 1. Base URL Configuration
Đảm bảo `base` trong `vite.config.js` khớp với tên repository:
```javascript
base: '/tên-repository-của-bạn/'
```

### 2. Router Configuration
App sử dụng `HashRouter` để tương thích với GitHub Pages:
```javascript
import { HashRouter } from 'react-router-dom'
```

### 3. Environment Variables
Để sử dụng các tính năng thanh toán thật, cần cấu hình:
```bash
VITE_STRIPE_PUBLIC_KEY=pk_live_...
VITE_VNPAY_MERCHANT_ID=...
VITE_MOMO_PARTNER_CODE=...
```

### 4. Mock Data
Hiện tại sử dụng mock data cho:
- User authentication
- Payment processing
- Analytics data

Để production thật, cần kết nối với backend APIs.

## 🎨 Customization

### Thay Đổi Branding
1. **Logo**: Thay file trong `/public/`
2. **Colors**: Cập nhật `tailwind.config.js`
3. **Fonts**: Cập nhật `index.html` và CSS
4. **Content**: Chỉnh sửa text trong components

### Thêm Tính Năng
1. Tạo component mới trong `/src/components/`
2. Thêm route trong `App.jsx`
3. Cập nhật navigation trong `Header.jsx`

## 🐛 Troubleshooting

### Build Errors
```bash
# Clear cache và reinstall
rm -rf node_modules package-lock.json
npm install
npm run build
```

### GitHub Pages Not Working
1. Kiểm tra repository là **Public**
2. Đảm bảo GitHub Actions đã chạy thành công
3. Kiểm tra `base` URL trong `vite.config.js`
4. Xem logs trong tab **Actions**

### Routing Issues
- GitHub Pages chỉ hỗ trợ client-side routing với `HashRouter`
- URLs sẽ có dạng: `/#/about` thay vì `/about`

## 📞 Support

Nếu gặp vấn đề trong quá trình deploy:

1. **Check GitHub Actions**: Xem logs trong tab Actions
2. **Verify Configuration**: Đảm bảo `vite.config.js` đúng
3. **Test Local**: Chạy `npm run build && npm run preview`
4. **Browser Console**: Kiểm tra errors trong DevTools

## 🎉 Demo Accounts

Để test các tính năng:

**Admin Account**:
- Email: `admin@minhkinhdat.com`
- Password: `admin123`

**User Account**:
- Email: `user@example.com`
- Password: `user123`

## 📈 Next Steps

Sau khi deploy thành công:

1. **Test All Features**: Đảm bảo mọi tính năng hoạt động
2. **Setup Analytics**: Google Analytics, Facebook Pixel
3. **Configure Real Payments**: Stripe, VNPay production keys
4. **Launch Marketing**: Theo marketing guide đã cung cấp
5. **Monitor Performance**: Uptime, speed, user feedback

---

**Chúc bạn deploy thành công! 🚀**

Nếu cần hỗ trợ thêm, vui lòng liên hệ qua GitHub Issues.
<!-- Updated for GitHub Pages -->
