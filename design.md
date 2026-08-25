# Hệ Thống Thiết Kế (Design System) - Phong Cách Karpathy.ai

Tài liệu này trích xuất toàn bộ phong cách thiết kế, hệ thống typography, bảng màu, layout và các thành phần giao diện (UI Components) từ website cá nhân của Andrej Karpathy ([karpathy.ai](https://karpathy.ai/)).

---

## 1. Triết Lý Thiết Kế (Design Philosophy)

* **Chủ nghĩa Tối giản Tuyệt đối (Pure Minimalism / Raw Web):** Không sử dụng framework UI nặng nề (no Bootstrap, no Tailwind, no React). Toàn bộ giao diện được xây dựng bằng Pure HTML & CSS thuần.
* **Tập trung vào Nội dung (Content-First):** Bố cục dạng dòng thời gian (Chronological Timeline) làm nổi bật quá trình phát triển sự nghiệp, nghiên cứu và các dự án lớn.
* **Tốc độ và Hiệu năng Tối đa (Ultra Fast & Lightweight):** Dung lượng tải trang cực nhỏ (~vài chục KB), không có script nặng, điểm Lighthouse đạt tuyệt đối 100/100.
* **Thanh lịch và Cổ điển (Timeless Aesthetic):** Kết hợp nét đơn giản của web thời kỳ đầu với hệ thống CSS Grid hiện đại.

---

## 2. Bảng Màu (Color Palette)

| Vai trò | Tên màu | Giá trị HEX | Mô tả & Ứng dụng |
| :--- | :--- | :--- | :--- |
| **Nền chính** | Background White | `#FFFFFF` | Nền trang tổng thể, tạo cảm giác sạch sẽ, thoáng đãng |
| **Chữ chính** | Body Text | `#333333` | Độ tương phản cao, dễ đọc, dịu mắt hơn màu đen tuyền `#000` |
| **Tiêu đề** | Heading Dark | `#111111` / `#000000` | Tiêu đề tên tác giả (H1), font weight bình thường |
| **Chữ phụ / Ngày tháng** | Muted Grey | `#666666` / `#777777` | Dùng cho cột mốc thời gian (`.timespan`), thông tin thứ cấp |
| **Liên kết (Links)** | Classic Link Blue | `#1A0DAB` / `#0066CC` | Màu xanh link truyền thống, có gạch chân hoặc hover tự nhiên |
| **Đường phân cách** | Border / Divider | `#EEEEEE` / `#E0E0E0` | Đường kẻ ngang `<hr>` mảnh và các đường viền nhẹ |
| **Điểm nhấn timeline** | Entry Dot | `#888888` / `#555555` | Điểm tròn đánh dấu sự kiện trên trục thời gian |

---

## 3. Typography (Kiểu Chữ)

### Font Stack
```css
font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
```
*Mặc định trên trang gốc:* `sans-serif` (dùng font hệ thống để tối ưu tốc độ tải và giữ nét tự nhiên của thiết bị).

### Phân cấp Kiểu chữ (Type Scale)

| Phần tử | Font Size | Line Height | Font Weight | Style | Ghi chú |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **H1 (Tên tác giả)** | `34px` (`2.125rem`) | `1.2` | `normal` (400) | Normal | Không in đậm, tạo nét khiêm tốn, trang nhã |
| **H2 (Tagline/Bio ngắn)**| `18px` - `20px` | `1.4` | `normal` (400) | *Italic* | Mô tả ngắn sở thích/chuyên môn + emoji |
| **Body (Nội dung)** | `16px` (`1rem`) | `1.4` - `1.5` | `normal` (400) | Normal | Khoảng cách dòng vừa phải, dễ quét mắt |
| **Timespan (Năm mốc)** | `15px` - `16px` | `1.4` | `bold` (600) hoặc 400 | Normal | Cột mốc thời gian (VD: `2024 -`, `2017 - 2022`) |
| **Links (`<a>`)** | Kế thừa | Kế thừa | Kế thừa | Underline khi cần | Màu xanh nổi bật, dễ nhận diện |

---

## 4. Hệ Thống Layout & Grid (CSS Grid & Breakpoints)

Trang web sử dụng hệ thống **12-column CSS Grid** kết hợp container cố định độ rộng trên màn hình lớn.

### Kích thước Container
* **Desktop (`min-width: 992px`):** `width: 970px; margin: 0 auto;`
* **Mobile / Tablet (`max-width: 991px`):** Chiều rộng `100%`, `padding: 0 15px;`

### Cấu trúc Grid 12 Cột
```css
.container {
    margin-left: auto;
    margin-right: auto;
    padding-left: 15px;
    padding-right: 15px;
}

@media (min-width: 992px) {
    .container {
        width: 970px;
    }
}

.row {
    display: grid;
    grid-template-columns: repeat(12, 1fr);
    gap: 10px; /* hoặc căn lề linh hoạt */
}
```

---

## 5. Chi Tiết Các Thành Phần Giao Diện (UI Components)

### 5.1. Phần Header (`#dhead`)
* **Desktop:** Chia tỉ lệ 6:6 (50% - 50%).
  * Cột trái (`#dpic`): Căn phải (`text-align: right`), chứa ảnh chân dung tròn `.ppic` (kích thước ~140px - 180px, bo tròn `border-radius: 50%`).
  * Cột phải (`#ddesc`): Căn trái (`text-align: left`, `padding-left: 20px`), chứa H1, H2, cụm icon mạng xã hội (`#dico`).
* **Mobile (`max-width: 991px`):** Cả 2 cột chuyển sang `grid-column: span 12;` và `text-align: center;`.

### 5.2. Hàng Icon Xã Hội (`#dico`)
* Chứa các icon SVG phẳng đơn sắc kích thước nhỏ (`.iico` ~ `20px` - `24px`).
* Khoảng cách giữa các icon: `margin-right: 8px;`.
* Icon Email có tính năng click để hiển thị địa chỉ email (chống bot thu thập dữ liệu tự động).

### 5.3. Trục Dòng Thời Gian (`#history` / `.entry.row`)
Mỗi mục công việc/sự kiện là một hàng `.entry.row` gồm 3 phần:
1. **`.timespan` (Khoảng 2 cột - Span 2):** Hiển thị năm (VD: `2023 - 2024`), căn lề phải trên Desktop.
2. **`.ico` (Khoảng 1-2 cột - Span 1/2):** Chứa logo công ty/trường học (Tesla, OpenAI, Stanford) kích thước nhỏ (~40px - 50px) kèm chấm mốc sự kiện (`.entry-dot`).
3. **`.desc` (Khoảng 8-9 cột - Span 8/9):** Mô tả chi tiết các thành tựu, video, bài viết, đường dẫn liên kết.

### 5.4. Thư Viện Media / Asset Nhúng (`.hassets`)
* Sử dụng để hiển thị các khung video tự phát hoặc ảnh chụp màn hình slide/talk.
* Bố trí theo dạng lưới tỉ lệ (VD: Video chính 50% chiều rộng, các slide phụ xếp 25% bên cạnh).

---

## 6. Mẫu Mã Nguồn Chuẩn (Template Boilerplate)

### 6.1. File `index.html`
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
  <title>Your Name</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>

  <!-- HEADER -->
  <header id="dhead" class="container">
    <div class="row">
      <div id="dpic">
        <img src="assets/profile.jpg" alt="Profile Picture" class="ppic">
      </div>
      <div id="ddesc">
        <h1>Your Name</h1>
        <h2>I like to build intelligent systems & write clean code 🚀</h2>
        <div id="dico">
          <a href="https://twitter.com/yourhandle" target="_blank" rel="noreferrer"><img src="assets/twitter.svg" class="iico" alt="Twitter"></a>
          <a href="https://github.com/yourhandle" target="_blank" rel="noreferrer"><img src="assets/github.svg" class="iico" alt="GitHub"></a>
          <a href="https://yourblog.com" target="_blank" rel="noreferrer"><img src="assets/rss.svg" class="iico" alt="Blog"></a>
          <img src="assets/email.svg" class="iico" id="iemail" title="Click to reveal email" style="cursor: pointer;" alt="Email">
        </div>
        <div id="demail"></div>
      </div>
    </div>
  </header>

  <hr>

  <!-- TIMELINE HISTORY -->
  <main id="history" class="container">

    <!-- Timeline Item 1 -->
    <div class="entry row">
      <div class="timespan">2024 - Present</div>
      <div class="ico">
        <img src="assets/company1.png" alt="Company Logo" class="cico">
      </div>
      <div class="desc">
        <strong>Lead AI Researcher</strong> at <a href="#">Lab Name</a>. Working on foundation models and scalable inference architectures.
      </div>
    </div>

    <!-- Timeline Item 2 -->
    <div class="entry row">
      <div class="timespan">2020 - 2024</div>
      <div class="ico">
        <img src="assets/company2.png" alt="Company Logo" class="cico">
      </div>
      <div class="desc">
        Senior Software Engineer at <a href="#">Tech Corp</a>. Designed and deployed distributed machine learning pipelines.
      </div>
    </div>

  </main>

  <script>
    // Email reveal logic
    document.getElementById('iemail')?.addEventListener('click', function() {
      const emailDiv = document.getElementById('demail');
      if (!emailDiv.innerText) {
        // Decode / display email safely
        emailDiv.innerText = 'youremail' + '@' + 'domain.com';
        emailDiv.style.marginTop = '6px';
        emailDiv.style.fontSize = '14px';
        emailDiv.style.color = '#666';
      }
    });
  </script>
</body>
</html>
```

### 6.2. File `style.css`
```css
/* --- RESET & BASE --- */
* {
  box-sizing: border-box;
}

body {
  margin: 0;
  padding: 0;
  background-color: #ffffff;
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
  font-size: 16px;
  line-height: 1.45;
  color: #333333;
}

a {
  color: #0066cc;
  text-decoration: underline;
}

a:hover {
  color: #004499;
}

hr {
  border: 0;
  border-top: 1px solid #eeeeee;
  margin: 30px auto;
  max-width: 970px;
}

/* --- LAYOUT GRID --- */
.container {
  margin-left: auto;
  margin-right: auto;
  padding-left: 15px;
  padding-right: 15px;
  max-width: 100%;
}

@media (min-width: 992px) {
  .container {
    width: 970px;
  }
}

.row {
  display: grid;
  grid-template-columns: repeat(12, 1fr);
  column-gap: 20px;
  row-gap: 15px;
}

/* --- HEADER SECTION --- */
#dhead {
  margin-top: 40px;
  margin-bottom: 20px;
}

#dpic {
  grid-column: span 6;
  text-align: right;
  display: flex;
  justify-content: flex-end;
  align-items: center;
}

.ppic {
  width: 160px;
  height: 160px;
  border-radius: 50%;
  object-fit: cover;
}

#ddesc {
  grid-column: span 6;
  display: flex;
  flex-direction: column;
  justify-content: center;
  padding-left: 10px;
}

h1 {
  font-size: 34px;
  font-weight: 400;
  margin: 0 0 6px 0;
  color: #111111;
}

h2 {
  font-size: 17px;
  font-weight: 400;
  font-style: italic;
  margin: 0 0 12px 0;
  color: #444444;
}

#dico {
  display: flex;
  align-items: center;
  gap: 10px;
}

.iico {
  width: 22px;
  height: 22px;
  opacity: 0.8;
  transition: opacity 0.15s ease;
}

.iico:hover {
  opacity: 1;
}

/* --- TIMELINE HISTORY --- */
#history {
  margin-bottom: 60px;
}

.entry {
  margin-bottom: 28px;
  align-items: flex-start;
}

.timespan {
  grid-column: span 2;
  font-size: 15px;
  color: #666666;
  text-align: right;
  padding-top: 2px;
}

.ico {
  grid-column: span 1;
  text-align: center;
}

.cico {
  width: 36px;
  height: 36px;
  object-fit: contain;
  border-radius: 4px;
}

.desc {
  grid-column: span 9;
  font-size: 15px;
  line-height: 1.5;
}

.desc ol, .desc ul {
  margin: 8px 0 8px 20px;
  padding: 0;
}

.desc li {
  margin-bottom: 4px;
}

/* --- RESPONSIVE MOBILE (<= 991px) --- */
@media (max-width: 991px) {
  #dhead {
    margin-top: 25px;
  }

  #dpic {
    grid-column: span 12;
    justify-content: center;
    text-align: center;
  }

  #ddesc {
    grid-column: span 12;
    padding-left: 0;
    text-align: center;
    align-items: center;
  }

  #dico {
    justify-content: center;
  }

  .timespan {
    grid-column: span 12;
    text-align: left;
    font-weight: 600;
    color: #444444;
  }

  .ico {
    grid-column: span 2;
    text-align: left;
  }

  .desc {
    grid-column: span 10;
  }
}
```

---

## 7. Ưu Điểm & Hướng Dẫn Áp Dụng

1. **Khả năng Bảo trì:** Không có build step phức tạp (không cần Webpack/Vite hay Node modules), chỉ cần chỉnh sửa trực tiếp trên file HTML.
2. **SEO & Hiển thị Thiết bị:** Tương thích 100% với mọi trình duyệt, hỗ trợ tốt cho trình đọc màn hình (Screen Readers) và bot tìm kiếm của Google/Bing.
3. **Phù hợp nhất cho:** Portfolio học thuật (Academic CV), Kỹ sư AI/Phần mềm, Nhà nghiên cứu, Blogger kỹ thuật muốn một trang chủ cá nhân cô đọng, chuyên nghiệp và tải trang ngay lập tức.
