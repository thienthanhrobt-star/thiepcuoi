# Thiệp Cưới – Next.js + Supabase

## Cài đặt
1. Tạo project tại https://supabase.com, mở **SQL Editor**, dán và chạy `supabase/schema.sql`.
2. **Authentication → Providers**: bật Email (và Google nếu muốn; cần Client ID/Secret từ Google Cloud).
3. **Authentication → URL Configuration**: Site URL = địa chỉ web của bạn; thêm `http://localhost:3000/**` và `https://tên-miền-của-bạn/**` vào Redirect URLs.
4. `cp .env.example .env.local`, điền URL và anon key (Project Settings → API).
5. `npm install && npm run dev` → http://localhost:3000
6. Triển khai: đưa lên GitHub, import vào Vercel, thêm 2 biến môi trường như trên.

## Trang quản trị (/admin)
1. Chạy thêm `supabase/admin.sql` trong SQL Editor (sau `schema.sql`).
2. Project Settings → API → copy **service_role key** vào `.env.local` (`SUPABASE_SERVICE_ROLE_KEY`). Khóa này rất nhạy cảm: không commit, không dùng tiền tố NEXT_PUBLIC_. Khi deploy Vercel, thêm nó vào Environment Variables.
3. Đăng nhập bằng tài khoản admin và vào `/admin`: xem tổng quan, khóa/mở khóa/xóa/đổi quyền tài khoản, tải lên mẫu thiệp (form hoặc file JSON, kèm ảnh xem trước).

## Tạo tài khoản quản trị
Đăng ký bình thường, rồi chạy trong SQL Editor:
`update profiles set role='admin' where id=(select id from auth.users where email='email-của-bạn');`

## Đã có / chưa có
Đã có: đăng ký, đăng nhập (email + Google), quên mật khẩu, bảo vệ trang, bảng điều khiển, CSDL + phân quyền (RLS), hàm cho khách mở thiệp và gửi RSVP.
Chưa có: trình tạo thiệp, trang `/t/[slug]` (nơi mẫu tải lên sẽ được dùng để hiển thị), email thông báo RSVP.

## Thư mục `demo/`
`demo/thiep-cuoi.html` là bản demo giao diện chạy độc lập (mở bằng trình duyệt, dữ liệu lưu trong trình duyệt). Không dùng cho sản phẩm thật.

## Đưa lên GitHub
Không bao giờ commit `.env.local` hay `SUPABASE_SERVICE_ROLE_KEY` (đã được `.gitignore` chặn).
