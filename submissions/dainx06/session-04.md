# Session 04 - Consensus & Blockchain Architecture

* Student: Nguyen Xuan Dai
* GitHub: @dainx06
* Submitted: 2026-11-11
* Commit: 

## 1. Summary
Hiểu các cơ chế đồng thuận (Consensus) giúp mạng lưới blockchain hoạt động phi tập trung nhưng vẫn nhất quán.Hiểu được các kiến trúc blockchain cơ bản, sự khác biệt giữa các mô hình lưu trữ và các giải pháp mở rộng (Layer 1, Layer 2).

## 2. Topic notes

**2.1 Consensus và bài toán Byzantine**
*   **Cơ chế đồng thuận:** Là cơ chế giúp các node trong một mạng phân tán đạt được sự thống nhất về trạng thái của sổ cái mà không cần tổ chức trung gian.
*   **Bài toán Tướng Byzantine (BFT - Byzantine Fault Tolerance):** Là một bài toán kinh điển trong hệ thống phân tán, giải quyết vấn đề làm sao để mạng lưới vẫn hoạt động đúng ngay cả khi có một số node bị lỗi hoặc cố tình hành động độc hại.

**2.2 Proof of Work và Proof of Stake**
*   **Proof of Work (PoW):** Cơ chế yêu cầu các thợ đào (miner) giải các bài toán mật mã phức tạp bằng sức mạnh máy tính để giành quyền tạo block mới (VD: Bitcoin). Tính bảo mật cao nhưng tiêu tốn nhiều năng lượng.
*   **Proof of Stake (PoS):** Cơ chế yêu cầu người tham gia (validator) "đặt cược" (stake) một lượng token nhất định để được quyền xác thực giao dịch (VD: Ethereum hiện tại). Tiết kiệm năng lượng và tốc độ xử lý nhanh hơn PoW.

**2.3 Finality**
*   **Finality (Tính hoàn tất):** Là sự đảm bảo rằng một giao dịch sau khi được đưa vào block sẽ không thể bị đảo ngược, thay đổi hay hủy bỏ. 
*   Trong PoW (như Bitcoin), finality là *xác suất* (probabilistic finality - cần đợi vài block xác nhận), trong khi một số cơ chế khác có *tính hoàn tất tuyệt đối* (deterministic finality).

**2.4 Trilemma, Layer 1 và Layer 2**
*   **Blockchain Trilemma:** Bộ ba bất khả thi của blockchain, bao gồm: *Phi tập trung (Decentralization), Bảo mật (Security) và Mở rộng (Scalability)*. Rất khó để một blockchain tối ưu cả 3 yếu tố này cùng lúc.
*   **Layer 1:** Mạng lưới blockchain cơ sở (VD: Bitcoin, Ethereum). Xử lý và ghi chép giao dịch trực tiếp.
*   **Layer 2:** Các giải pháp mở rộng được xây dựng trên Layer 1 (VD: Lightning Network, Rollups) nhằm tăng tốc độ xử lý giao dịch và giảm phí mà vẫn dựa vào bảo mật của Layer 1.

**2.5 Account-based và UTXO**
*   **UTXO (Unspent Transaction Output):** Mô hình giống như "tiền mặt". Bạn nhận các tờ tiền (UTXO) và khi tiêu, bạn đưa toàn bộ tờ tiền đó, phần dư sẽ được trả lại thành một UTXO mới (VD: Bitcoin). Dễ theo dõi nguồn gốc và bảo mật tốt.
*   **Account-based:** Mô hình giống như "tài khoản ngân hàng". Hệ thống theo dõi số dư của từng địa chỉ ví và cập nhật trạng thái trực tiếp. Dễ dàng để lập trình Smart Contract (VD: Ethereum).

**2.6 Public, Private, Permissioned Blockchain**
*   **Public Blockchain:** Mạng công khai, ai cũng có thể tham gia đọc/ghi dữ liệu và trở thành node (Bitcoin, Ethereum).
*   **Private Blockchain:** Mạng khép kín, được kiểm soát bởi một tổ chức duy nhất, tốc độ nhanh, bảo mật nội bộ nhưng không phi tập trung.
*   **Permissioned (Consortium) Blockchain:** Mạng lai, chỉ những node được cấp quyền mới được tham gia xác thực giao dịch, thường dùng cho liên minh các doanh nghiệp.

## 3. Work completed

## 4. Evidence

## 5. Blockers

## 6. Takeaway
*   Mọi blockchain đều phải đánh đổi giữa các yếu tố trong Trilemma. Việc hiểu rõ điểm mạnh yếu của PoW/PoS, Layer 1/Layer 2 và UTXO/Account-based giúp dev lựa chọn đúng nền tảng để xây dựng dApp sau này.
