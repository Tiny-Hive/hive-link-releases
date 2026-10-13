# Hive Link — tệp cài app Tiny Hive

Kho này chỉ chứa **tệp cài và mã băm** của app Tiny Hive (Hive Link), không có mã nguồn.

Hive Link cho bot của bạn gọi công cụ chạy ngay trên máy bạn: đọc/ghi thư mục bạn cho phép, build iOS/Android, server MCP riêng. Mỗi lần bot xin chạy, bạn duyệt trên app.

## Bản nào cho máy nào

| Máy | Tệp | Trạng thái |
|---|---|---|
| macOS, chip Apple (M1 trở lên) | `hive-link-app-macos-<bản>.dmg` | có |
| Windows 10/11 64-bit (x64) | `hive-link-app-windows-x64-<bản>-setup.exe` | có |

Tải ở mục **Releases** (bên phải trang này), bản mới nhất, cùng tệp `SHA256SUMS.txt`.

App tự kiểm bản mới mỗi lần mở (Mac qua Sparkle, Windows qua WinSparkle) và báo khi có bản mới hơn — không cần tự tải lại thủ công, trừ lần cài đầu tiên.

## Cần có trước

- Tài khoản Control Plane của Tiny Hive (đăng nhập bằng mã gửi về email). Chưa có thì xin người quản trị.

## Cài trên Mac

1. Tải `hive-link-app-macos-<bản>.dmg` và `SHA256SUMS.txt` vào thư mục Downloads.
2. Kiểm mã băm, dán vào Terminal (phải in ra `OK`):
   ```
   cd ~/Downloads && grep macos SHA256SUMS.txt | shasum -a 256 -c
   ```
   In ra `FAILED` thì dừng lại, không cài.
3. Nháy đúp tệp `.dmg`, kéo **Tiny Hive** vào **Applications**.
4. Mở app lần đầu: macOS chặn vì app chưa ký với Apple → bấm Done → System Settings → Privacy & Security → **Open Anyway**. Cho phép thông báo.
5. Trong app bấm **Add account**:
   - Control Plane address: `https://okiya-api.superunderwear.org`
   - Machine name there: tên riêng cho máy, 2–16 ký tự `a-z`, `0-9`, `-`
   - Continue → **Open in browser** → đăng nhập Control Plane → nhập mã → **Allow**.
6. Màn **This machine**: gõ tên bot vào ô *Bind a bot* → Bind.
7. Kiểm tra: màn This machine báo Link **online**; nhờ bot gọi thử một công cụ → hộp duyệt hiện trên máy → **Allow once** → bot nhận được kết quả.

Hộp duyệt: **Allow once** (lần này), **Always allow** (luôn cho cả server), **Deny**; để quá 2 phút không trả lời thì tự từ chối. Mỗi server MCP chạy với toàn quyền tài khoản máy của bạn: chỉ cho bot bạn tin.

## Cài trên Windows

1. Tải `hive-link-app-windows-x64-<bản>-setup.exe` và `SHA256SUMS.txt` vào thư mục Downloads.
2. Kiểm mã băm, dán vào PowerShell (phải in ra `True`):
   ```powershell
   cd $HOME\Downloads
   $expected = (Select-String -Path SHA256SUMS.txt -Pattern 'windows').Line.Split(' ')[0]
   (Get-FileHash .\hive-link-app-windows-x64-*-setup.exe -Algorithm SHA256).Hash -eq $expected.ToUpper()
   ```
   In ra `False` thì dừng lại, không cài.
3. Chạy tệp `-setup.exe`, Windows SmartScreen chặn vì app chưa ký nhà phát hành đã-xác-minh → bấm **More info** → **Run anyway**. Theo wizard tới khi cài xong.
4. Mở app lần đầu, bấm **Add account**:
   - Control Plane address: `https://okiya-api.superunderwear.org`
   - Machine name there: tên riêng cho máy, 2–16 ký tự `a-z`, `0-9`, `-`
   - Continue → **Open in browser** → đăng nhập Control Plane → nhập mã → **Allow**.
5. Màn **This machine**: gõ tên bot vào ô *Bind a bot* → Bind.
6. Kiểm tra: màn This machine báo Link **online**; nhờ bot gọi thử một công cụ → hộp duyệt hiện trên máy → **Allow once** → bot nhận được kết quả.

## Gặp lỗi

- Mac: không thấy nút Open Anyway: `xattr -dr com.apple.quarantine "/Applications/Tiny Hive.app"` rồi mở lại app.
- Windows: SmartScreen chặn lại sau khi cài xong (chạy app lần đầu) → bấm **More info** → **Run anyway**, chỉ cần làm một lần.
- Trang Control Plane báo tên máy đã có người dùng: trong app bấm **Change name**.
