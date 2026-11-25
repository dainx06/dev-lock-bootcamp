# Session 06

* Student: Nguyen Xuan Dai
* GitHub: [@dainx06](https://github.com/dainx06)
* Submitted: 2026-11-25
* Commit: [S06] add devlog - @dainx06

## 1. Summary
* **Kiến trúc 4 lớp của dApp**: Phân tích luồng hoạt động từ `Frontend → Wallet → Smart Contract → Blockchain (qua RPC)` và tính độc lập của dữ liệu on-chain khi giao diện web ngừng hoạt động.
* **Cơ chế Đọc (Read) vs. Ghi (Write) & Phân quyền ví**: Phân biệt truy vấn miễn phí gas với giao dịch thay đổi trạng thái mất phí gas; làm rõ ranh giới bảo mật giữa `Connect Wallet`, `Sign Message` và `Approve Token`.
* **Hệ sinh thái Web3 & Oracle**: Tìm hiểu cách vận hành của các mảng ứng dụng cốt lõi (DeFi, Payment, NFT, Gaming, DAO) cùng vai trò cầu nối dữ liệu thực tế của Oracle.
* **Thực hành Mini Demo trên Testnet**: Viết, biên dịch và triển khai hợp đồng thông minh `ClassroomSeat.sol` trên Remix VM và Ethereum Sepolia Testnet, sau đó đối chiếu kết quả trên Etherscan.

## 2. Topic notes

### 2.1. dApp Architecture: Frontend → Wallet → Smart Contract → Blockchain
* **Khái niệm dApp (Decentralized Application)**: Là ứng dụng có phần logic nghiệp vụ cốt lõi và trạng thái dữ liệu được vận hành bởi Smart Contract trên Blockchain thay vì máy chủ tập trung truyền thống.
* **Luồng tương tác 4 lớp**:
  1. **Frontend (Giao diện)**: Nơi người dùng thao tác (HTML/CSS/JS, React...). Frontend hiển thị dữ liệu và đóng gói yêu cầu giao dịch gửi sang ví.
  2. **Wallet (Ví Web3)**: Trung gian xác thực danh tính (như MetaMask). Ví hiển thị chi tiết lệnh (mạng, địa chỉ nhận, phí gas) để người dùng kiểm tra và dùng Private Key ký xác nhận.
  3. **Smart Contract (Hợp đồng thông minh)**: Chứa toàn bộ quy tắc, điều kiện kiểm tra (`require`) và logic xử lý được lập trình sẵn trên chuỗi.
  4. **Blockchain & RPC Node**: Cổng RPC (Remote Procedure Call) chuyển tiếp yêu cầu từ ví/frontend vào mạng lưới. Các node xác thực và ghi nhận sự thay đổi trạng thái vào sổ cái vĩnh viễn.
* **Tính phi tập trung khi Frontend gặp sự cố**: Nếu trang web bị sập hoặc tắt máy chủ, dApp vẫn tồn tại vì dữ liệu và code nằm trên Blockchain. Người dùng hoàn toàn có thể tương tác trực tiếp với Smart Contract thông qua các công cụ như Etherscan hoặc Remix IDE.

---

### 2.2. Phân biệt Read vs. Write & Các quyền ký ví (Connect, Sign, Approve)

**1. Cơ chế Đọc (Read) vs. Ghi (Write) dữ liệu:**
* **Read (Đọc / `eth_call`)**: Truy vấn trạng thái có sẵn trên sổ cái qua cổng RPC (ví dụ: xem số dư, kiểm tra trạng thái đăng ký). Không tạo giao dịch on-chain, **không cần ký ví** và **miễn phí gas**.
* **Write (Ghi / Transact)**: Gửi lệnh làm thay đổi trạng thái trên Blockchain (ví dụ: chuyển token, gọi hàm ghi dữ liệu). Bắt buộc phải có **chữ ký xác thực từ ví** và **tốn phí gas** trả cho mạng lưới.

**2. Ba cấp độ phân quyền khi tương tác với ví:**
* **Connect Wallet (Kết nối ví)**: Chỉ chia sẻ địa chỉ ví công khai (Public Address) và mạng đang chọn để website nhận diện tài khoản. Thao tác này **không cấp quyền rút hay chuyển tiền**.
* **Sign Message (Ký thông điệp)**: Ký xác nhận một chuỗi văn bản off-chain để chứng minh quyền sở hữu ví (không tốn gas). *Lưu ý bảo mật*: Cần đọc kỹ nội dung ký để tránh ký nhầm các chuẩn chữ ký cấp quyền ngầm (như `Permit`) cho phép kẻ xấu rút token sau này.
* **Approve Token (Cấp hạn mức chi tiêu - Allowance)**: Là một giao dịch on-chain cho phép một Smart Contract khác (Spender) được tự động trích một lượng token tối đa từ ví của bạn.
  * *Nguyên tắc an toàn*: Việc ngắt kết nối (Disconnect) ví khỏi trang web **không hủy bỏ quyền Approve**. Muốn thu hồi bắt buộc phải thực hiện lệnh **Revoke** (đặt hạn mức về `0`) trên chuỗi.

---

### 2.3. Hệ sinh thái Web3: DeFi, Payment, NFT, Gaming, DAO
* **DeFi (Tài chính phi tập trung)**: Hệ thống tài chính mở không qua ngân hàng, hoạt động qua Smart Contract (sàn giao dịch phi tập trung DEX, bể thanh khoản Liquidity Pool, vay/cho vay Lending).
* **Payment (Thanh toán Web3)**: Chuyển giá trị xuyên biên giới nhanh chóng, minh bạch với chi phí tối ưu thông qua Stablecoin hoặc Native Coin.
* **NFT (Non-Fungible Token)**: Tài sản số độc nhất dùng để chứng minh quyền sở hữu vật phẩm số, tác phẩm nghệ thuật, vé sự kiện hoặc chứng chỉ trên Blockchain.
* **Gaming (GameFi)**: Ứng dụng Blockchain vào trò chơi giúp người chơi thực sự sở hữu vật phẩm trong game dưới dạng NFT/Token và tự do giao dịch.
* **DAO (Tổ chức tự trị phi tập trung)**: Mô hình quản trị cộng đồng minh bạch, nơi các thành viên nắm giữ token quản trị có quyền đề xuất và biểu quyết các quyết định chung thông qua Smart Contract.

---

### 2.4. Oracle (Cung cấp dữ liệu off-chain)
* **Vai trò**: Smart Contract chạy trong môi trường khép kín trên Blockchain nên không thể tự truy cập internet để lấy dữ liệu thế giới thực (như tỷ giá ngoại tệ, giá coin theo thời gian thực, kết quả thể thao, thời tiết). **Oracle** đóng vai trò là cầu nối đưa dữ liệu ngoại vi (off-chain) vào trong Blockchain (on-chain).
* **Rủi ro cần lưu ý**: Tính chính xác của Smart Contract phụ thuộc hoàn toàn vào nguồn dữ liệu đầu vào. Nếu Oracle bị tấn công, cung cấp dữ liệu sai hoặc cập nhật quá trễ, Smart Contract sẽ thực thi sai lệch gây thiệt hại tài sản.

---

### 2.5. Mini Demo: Tương tác Smart Contract trên Testnet

**Bước 1: Viết và biên dịch hợp đồng trên Remix IDE**
* Tạo file `ClassroomSeat.sol` và biên dịch với phiên bản Solidity `0.8.24`:
```solidity
// SPDX-License-Identifier: MIT
pragma solidity 0.8.24;

contract ClassroomSeat {
    mapping(address => bool) public registered;
    uint256 public totalRegistered;

    event Registered(address indexed attendee, uint256 total);

    function register() external {
        require(!registered[msg.sender], "Already registered");
        registered[msg.sender] = true;
        totalRegistered += 1;
        emit Registered(msg.sender, totalRegistered);
    }
}
## 3. Work completed
Nắm vững kiến trúc 4 lớp của dApp và luồng đi của một lệnh giao dịch từ giao diện xuống sổ cái Blockchain.
Phân biệt rõ ràng thao tác Đọc (eth_call) và Ghi (Transact), cùng các rủi ro bảo mật liên quan đến Sign Message và Approve Token.
Hiểu được bức tranh tổng quan các mảnh ghép Web3 (DeFi, Payment, NFT, Gaming, DAO) và cơ chế hoạt động của Oracle.
Hoàn thành triển khai và kiểm thử thực tế Smart Contract ClassroomSeat.sol trên cả Remix VM và Sepolia Testnet.
## 4. Evidence
N/A
## 5. Blockers
## 6. Takeaway
