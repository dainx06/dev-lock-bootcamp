# Session 05 - Smart Contracts & Digital Assets

- Student: Nguyen Xuan Dai
- GitHub: @dainx06
- Submitted: 2026-11-18
- Commit:[S05] add devlog - @dainx06

## 1. Summary

Hiểu smart contract là chương trình chạy trực tiếp trên blockchain và là nền tảng để tạo ra các tài sản số. Phân biệt được coin gốc của một mạng với token do smart contract tạo ra, biết cách token được tạo thêm (mint) hoặc hủy bớt (burn), và hiểu stablecoin, NFT là gì. Mình cũng hiểu phí gas là chi phí để mạng chạy giao dịch, và biết sơ lược về các máy ảo EVM, SVM, WASM nơi smart contract được thực thi.

## 2. Topic notes

## 2. Topic notes

### 2.1 Smart Contract
- **Khái niệm:** Smart Contract (Hợp đồng thông minh) là các đoạn mã/chương trình tự động thực thi được lưu trữ và chạy trực tiếp trên mạng lưới blockchain.
- **Cơ chế hoạt động:** Hoạt động theo logic điều kiện **"If – Then"** (nếu điều kiện đầu vào thỏa mãn thì tự động thực thi hành động tương ứng) mà không cần bên trung gian kiểm soát.
- **Đặc điểm cốt lõi:**
  - **Tự động hóa (Autonomous):** Tự chạy ngay khi nhận được giao dịch kích hoạt hợp lệ.
  - **Bất biến (Immutable):** Sau khi triển khai (deploy) lên blockchain, mã nguồn không thể bị chỉnh sửa tùy ý.
  - **Minh bạch & Phi tập trung:** Mọi người đều có thể kiểm tra mã nguồn/trạng thái, và kết quả thực thi được toàn bộ các node trong mạng xác thực đồng thuận.

### 2.2 Native Coin và Token
- **Native Coin (Đồng tiền gốc):**
  - Là đồng tiền mã hóa nguyên bản gắn liền với một mạng blockchain độc lập (Layer 1), được tích hợp sẵn ở tầng giao thức (protocol level).
  - **Ví dụ:** BTC (Bitcoin), ETH (Ethereum), SOL (Solana).
  - **Vai trò:** Dùng để thanh toán phí giao dịch (Gas/Transaction Fee), trả thưởng cho miner/validator để bảo mật mạng lưới và làm phương tiện trao đổi cơ bản.
- **Token:**
  - Là tài sản số được tạo ra và quản lý thông qua Smart Contract trên một nền tảng blockchain có sẵn (không sở hữu blockchain riêng).
  - Tuân theo các bộ tiêu chuẩn kỹ thuật (Token Standards) như **ERC-20** (Ethereum), **SPL** (Solana), **BEP-20** (BNB Chain).
  - **Ví dụ:** USDT, LINK, UNI.
  - **Vai trò:** Đại diện cho quyền quản trị (Governance), tiện ích trong ứng dụng (Utility), điểm thưởng hoặc tài sản thế giới thực được số hóa (RWA).

### 2.3 Mint và Burn
- **Mint (Đúc / Phát hành mới):**
  - Là hành động gọi hàm trong Smart Contract để tạo ra một lượng token hoặc NFT mới và đưa vào lưu thông, làm tăng tổng nguồn cung (Total Supply).
  - Thường diễn ra khi khởi tạo tài sản, người dùng nạp tài sản thế chấp (để mint stablecoin), nhận phần thưởng staking hoặc tạo một NFT mới.
- **Burn (Đốt / Tiêu hủy):**
  - Là hành động loại bỏ vĩnh viễn một lượng coin/token khỏi lưu thông bằng cách giảm tổng cung trong Smart Contract hoặc gửi token đến một địa chỉ ví không có khóa riêng tư (**Burn Address**, ví dụ: `0x0000...dead`).
  - **Mục đích:** Kiểm soát lạm phát, tạo sự khan hiếm, giữ tỷ giá neo của stablecoin khi người dùng rút tiền pháp định, hoặc cơ chế đốt một phần phí giao dịch (như EIP-1559 trên Ethereum).

### 2.4 Stablecoin
- **Khái niệm:** Là loại token được thiết kế để duy trì giá trị ổn định, thường neo giá (peg) theo tỷ lệ 1:1 với một tài sản ổn định bên ngoài như tiền pháp định (USD, EUR) hoặc vàng.
- **Vai trò:** Khắc phục sự biến động giá mạnh của các đồng crypto truyền thống, giúp thuận tiện trong thanh toán, lưu trữ giá trị và giao dịch trong DeFi.
- **Các nhóm Stablecoin chính:**
  - **Thế chấp bằng tiền pháp định (Fiat-backed):** Được bảo chứng 1:1 bằng tiền mặt hoặc trái phiếu chính phủ trong ngân hàng (VD: **USDT**, **USDC**).
  - **Thế chấp bằng tài sản mã hóa (Crypto-backed):** Được bảo chứng vượt mức (over-collateralized) bằng các đồng crypto khác thông qua Smart Contract (VD: **DAI**).
  - **Thuật toán (Algorithmic):** Sử dụng thuật toán cung – cầu tự động (mint/burn) qua smart contract để điều tiết giá trị mà không cần hoặc cần rất ít tài sản thế chấp.

### 2.5 NFT
- **Khái niệm:** **NFT (Non-Fungible Token)** là token không thể thay thế. Mỗi NFT là một tài sản số độc nhất trên blockchain với mã định danh (**Token ID**) và siêu dữ liệu (**Metadata**) riêng biệt, không thể hoán đổi ngang giá 1:1 với nhau như tiền tệ thông thường (Fungible Token).
- **Tiêu chuẩn phổ biến:** **ERC-721** (mỗi token là duy nhất) và **ERC-1155** (hỗ trợ cả token độc nhất lẫn bán thay thế - semi-fungible) trên Ethereum.
- **Ứng dụng:** Chứng nhận quyền sở hữu và tính xác thực cho tác phẩm nghệ thuật số, vật phẩm game (GameFi), vé sự kiện, tên miền Web3, chứng chỉ học thuật.

### 2.6 Gas và Transaction Fee
- **Gas:**
  - Là đơn vị đo lường khối lượng tính toán và tài nguyên (CPU, bộ nhớ, lưu trữ) cần thiết để thực hiện một giao dịch hoặc chạy một hàm trong Smart Contract trên blockchain (đặc biệt trong hệ sinh thái EVM).
  - Thao tác càng phức tạp (như swap token, mint NFT) thì tốn càng nhiều Gas hơn so với chuyển coin thông thường (chuyển ETH cơ bản tốn `21,000` gas).
- **Transaction Fee (Phí giao dịch):**
  - Là chi phí thực tế (trả bằng Native Coin như ETH, SOL) mà người dùng phải trả để giao dịch được validator/miner xử lý và ghi vào khối.
  - **Công thức trên EVM:** `Transaction Fee = Gas Used × Gas Price`
  - **Mục đích:** Trả công cho các node vận hành mạng lưới và ngăn chặn tình trạng spam giao dịch hoặc vòng lặp vô tận làm tê liệt hệ thống.

### 2.7 EVM, SVM, WASM
Đây là các **môi trường thực thi / máy ảo (Execution Environments)** đóng vai trò như "bộ xử lý" phi tập trung để biên dịch và chạy mã Smart Contract:
- **EVM (Ethereum Virtual Machine):**
  - Máy ảo tiêu chuẩn của Ethereum và các mạng tương thích (BNB Chain, Polygon, Arbitrum, Optimism...).
  - Ngôn ngữ lập trình chính: **Solidity**, Vyper. Có hệ sinh thái công cụ và cộng đồng phát triển lớn nhất hiện nay.
- **SVM (Solana Virtual Machine):**
  - Môi trường thực thi hiệu năng cao của mạng Solana.
  - Điểm nổi bật: Hỗ trợ xử lý giao dịch **song song (parallel execution)**, cho thông lượng rất cao và phí giao dịch thấp. Ngôn ngữ chính: **Rust**, C/C++.
- **WASM (WebAssembly):**
  - Chuẩn mã nhị phân hiệu suất cao được nhiều blockchain thế hệ mới (Polkadot, Cosmos/CosmWasm, Near, Arbitrum Stylus) tích hợp làm môi trường chạy Smart Contract.
  - Điểm nổi bật: Cho phép viết Smart Contract bằng nhiều ngôn ngữ phổ biến (Rust, C/C++, Go, AssemblyScript...) với tốc độ thực thi gần với mã máy gốc.

## 3. Work completed

## 4. Evidence

## 5. Blockers

## 6. Takeaway
- **Tư duy lập trình hóa trên Blockchain:** Smart Contract biến blockchain từ một sổ cái lưu trữ giao dịch đơn thuần thành một nền tảng tính toán phi tập trung có thể lập trình được, là nền móng cho toàn bộ hệ sinh thái DApp và DeFi.
- **Phân biệt rõ kiến trúc tài sản số:** Nắm vững sự khác biệt giữa **Native Coin** (gắn với hạ tầng Layer 1, dùng trả phí) và **Token / NFT** (được tạo ra bởi Smart Contract theo các chuẩn như ERC-20, ERC-721), cùng cơ chế **Mint/Burn** để điều tiết nguồn cung.
- **Hiểu bản chất chi phí và hạ tầng thực thi:** Gas không phải là một đồng tiền mà là thước đo tài nguyên tính toán giúp chống spam mạng lưới; đồng thời việc nhận diện sự khác biệt giữa **EVM**, **SVM** và **WASM** giúp định hướng chọn ngôn ngữ (Solidity hay Rust) và hệ sinh thái phù hợp khi bắt tay vào lập trình Smart Contract sau này.
