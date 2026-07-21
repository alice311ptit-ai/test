# Chợ 4.0 — Wireframe báo doanh thu và nộp lệ phí

Bản wireframe tương tác (low-fidelity) cho luồng tiểu thương chợ truyền thống khai doanh thu hàng tháng và nộp lệ phí chợ.

**10 màn**, khung máy **iPhone 12 Pro Max (428 × 926 pt)**, bấm được theo luồng thật.

Toàn bộ việc khai báo gộp trong **một màn duy nhất** — người dùng cuộn thay vì chuyển qua nhiều bước.

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
| Khai báo | 1 | Tổng quan — một nút dẫn thẳng vào khai báo |
| | 2 | **Báo doanh thu (màn gộp)** — hạn báo, sạp, câu hỏi có bán hàng, chọn mức tiền theo tháng hoặc theo ngày, lệ phí |
| | 3 | Đã ghi nhận |
| | 4 | Không phải nộp (nhánh nghỉ bán) |
| | 5 | Lịch sử |
| Nộp lệ phí | 6–10 | Nộp lệ phí, đang kiểm tra, đã nộp xong, đang kiểm tra với ngân hàng, chuyển tiền chưa xong |

### Màn gộp hoạt động thế nào

Mặc định chọn sẵn **Có bán hàng**, nên trường hợp phổ biến chỉ cần **2 lần chạm**: chọn mức doanh thu, rồi bấm gửi.

- **Theo tháng** — 5 chip: dưới 10 triệu · 10–20 · 20–30 · trên 30 · số khác (mở ô nhập)
- **Theo ngày** — chọn doanh thu một ngày và số ngày bán, hệ thống tự quy ra mức tháng
- Lệ phí tính lại ngay khi đổi lựa chọn; nút gửi chỉ bật khi đã chọn mức
- Chọn **Nghỉ, không bán** thì phần doanh thu ẩn đi, thay bằng hai lý do nghỉ:
  - **Nghỉ tạm** → vẫn phải nộp mức tối thiểu (lệ phí chợ tối thiểu 100k + bảo hiểm 50k = 150k), đi tiếp sang nộp lệ phí
  - **Nghỉ hẳn, trả sạp** → không phải nộp, kết thúc luôn

Ba nhóm điều khiển (có bán hàng / nghỉ bán, theo tháng / theo ngày, và các chip mức tiền) đều cao **56px** — bằng nhau và vẫn đạt ngưỡng vùng chạm tối thiểu. Chip xếp **3 + 2 trên đúng 2 dòng**.

### Màn nộp lệ phí

- **Mã QR hiện sẵn** ngay dưới số tiền, để người dùng chụp lại và quét bằng máy khác nếu muốn
- **Danh sách ngân hàng**, ngân hàng hay dùng đẩy lên đầu kèm nhãn *Hay dùng*
- Câu hướng dẫn đặt **ngay trên nút**, đọc xong là bấm
- Nút chính: **Mở ngân hàng đóng phí**

Mã QR trong demo là hoa văn minh hoạ, không quét ra dữ liệu thật. Màu mã QR cố định để giữ độ tương phản cho máy quét — không đổi theo `--brand`.

Mức lệ phí trong demo (100k / 150k / 200k / 300k + bảo hiểm 50k) là **số giả định** để thấy cơ chế, chưa phải biểu phí thật.

Mỗi màn có phần chú thích bên dưới máy: **node tương ứng trong user flow** và **lý do thiết kế**.

Ở màn 7 (*Đang kiểm tra*) có ba nút demo để chọn kết quả giao dịch — đây là công cụ trình bày, không phải phần của sản phẩm.

---

## Điều hướng

- Bấm các nút trong máy để đi theo luồng
- Nút back trong app quay lại màn trước
- Cột trái nhảy thẳng tới bất kỳ màn nào
- URL có `#tên-màn`, copy được để gửi thẳng tới một màn cụ thể

---

## Lưu ý về nội dung

**Business rule cần xác minh với ban quản lý chợ:**

1. Lệ phí có phần cố định theo sạp, hay hoàn toàn phụ thuộc doanh thu — quyết định nhánh "lệ phí = 0"
2. Các mức doanh thu và biểu phí tương ứng
3. Quyền chỉnh sửa sau khi đã gửi kê khai
4. Ngân hàng phổ biến tại chợ có hỗ trợ deeplink điền sẵn không — nếu không, màn 6 phải quay lại QR làm mặc định

Luồng này **không bao gồm khai hộ**. Nếu cần, đó là một luồng riêng.

Số liệu, tên người và tên chợ trong bản demo đều là ví dụ.
