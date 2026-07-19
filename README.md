# Chợ 4.0 — Wireframe báo doanh thu và nộp lệ phí

Bản wireframe tương tác (low-fidelity) cho luồng tiểu thương chợ truyền thống khai doanh thu hàng tháng và nộp lệ phí chợ.

**21 màn**, khung máy **iPhone 12 Pro Max (428 × 926 pt)**, bấm được theo luồng thật.

---

## Đưa lên GitHub Pages

Chỉ có một file `index.html`, không cần build, không cần cài gì.

```bash
git init
git add .
git commit -m "Wireframe Chợ 4.0"
git branch -M main
git remote add origin https://github.com/<tài-khoản>/<tên-repo>.git
git push -u origin main
```

Sau đó vào repo trên GitHub:

**Settings → Pages → Build and deployment → Source: `Deploy from a branch` → Branch: `main` / `(root)` → Save**

Đợi khoảng 1 phút, link demo sẽ là:

```
https://<tài-khoản>.github.io/<tên-repo>/
```

> Repo để **Public** thì link mới mở được cho người ngoài. Nếu để Private, GitHub Pages yêu cầu tài khoản trả phí.

Muốn thử trước khi push, mở thẳng `index.html` bằng trình duyệt là chạy được.

---

## Đổi màu branding

Mở `index.html`, sửa **đúng một dòng** ở đầu khối `<style>`:

```css
:root{
  --brand:#16181D;      /* ← đổi mã màu ở đây */
  --on-brand:#FFFFFF;   /* màu chữ nằm trên nền brand */
}
```

`--brand` áp cho: nút chính, viền trạng thái được chọn, chấm radio, badge thành công, và mục đang mở ở cột trái.

Nếu màu branding sáng (vàng, cam nhạt…), đổi `--on-brand` sang `#16181D` để chữ trên nút vẫn đọc được.

Mặc định để gần đen vì đây là bản **low-fidelity** — mục đích là người xem đọc cấu trúc chứ không bị hút vào màu sắc.

---

## Cấu trúc

| Nhóm | Màn | Nội dung |
|---|---|---|
| Chặng 1 | 1–4 | Vào luồng: trang chủ, chi tiết kỳ, chọn sạp, hỏi có bán hàng không |
| Chặng 2 | 5–8 | Báo doanh thu: so với tháng trước, ước tính theo ngày, khoảng đề xuất, nhánh nghỉ bán |
| Chặng 3 | 9–12 | Ghi nhận: xem lại, đã ghi nhận, miễn lệ phí, lịch sử |
| Chặng 4 | 13–17 | Nộp tiền: thông tin trả, đang kiểm tra, thành công, đang kiểm tra với ngân hàng, thất bại |
| Khai hộ | 18–21 | Giả thuyết: trang chủ người khai hộ, xem lại, đã gửi, chủ sạp nhận thông báo |

Mỗi màn có phần chú thích bên dưới máy: **node tương ứng trong user flow** và **lý do thiết kế**.

Ở màn 14 (*Đang kiểm tra*) có ba nút demo để chọn kết quả giao dịch — đây là công cụ trình bày, không phải phần của sản phẩm.

---

## Điều hướng

- Bấm các nút trong máy để đi theo luồng
- Nút back trong app quay lại màn trước
- Cột trái nhảy thẳng tới bất kỳ màn nào
- URL có `#tên-màn`, copy được để gửi thẳng tới một màn cụ thể

---

## Lưu ý về nội dung

**Nhóm màn khai hộ (18–21) là giả thuyết, chưa được kiểm chứng.** Có ba mô hình khả dĩ — mượn máy chủ sạp, uỷ quyền có đăng ký, hoặc link một lần — và bản này thể hiện mô hình thứ hai với cơ chế *ghi nhận ngay + báo qua Zalo + cửa sổ phản đối*. Cần phỏng vấn để chốt mô hình trước khi thiết kế chi tiết.

**Business rule cần xác minh với ban quản lý chợ:**

1. Lệ phí có phần cố định theo sạp, hay hoàn toàn phụ thuộc doanh thu — quyết định nhánh "lệ phí = 0"
2. Chủ sạp có bắt buộc xác nhận khi người khác khai hộ không
3. Quyền chỉnh sửa sau khi đã gửi kê khai
4. Ngân hàng phổ biến tại chợ có hỗ trợ deeplink điền sẵn không — nếu không, màn 13 phải quay lại QR làm mặc định

Số liệu, tên người và tên chợ trong bản demo đều là ví dụ.
