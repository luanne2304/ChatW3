# ChatW3
Giới Thiệu

Đây là hệ thống smart contract hỗ trợ nhắn tin cá nhân và nhắn tin nhóm sử dụng mã hóa. Hệ thống bao gồm các hợp đồng:

Factory: Quản lý người dùng và nhóm.

UserContract: Hợp đồng cá nhân của mỗi người dùng.

GroupChat: Hợp đồng quản lý nhóm chat.

1. Cài Đặt & Triển Khai

Yêu cầu

Solidity ^0.8.19

Triển khai

2. Luồng Hoạt Động

2.1 Đăng ký người dùng

Người dùng gọi registerUser(publicKey, encryptedPrivateKey)

Hợp đồng tạo UserContract mới

Lưu thông tin người dùng vào users mapping

2.2 Tạo nhóm chat

Người dùng gọi createGroup(groupPublicKey, encryptedGroupPrivateKey)

Hợp đồng kiểm tra người dùng có tồn tại không

Tạo hợp đồng GroupChat

Lưu thông tin nhóm vào groups

2.3 Gửi và nhận tin nhắn cá nhân

Người dùng gửi tin nhắn bằng sendMessage(encryptedMessage)

Tin nhắn được lưu vào messages

Chủ sở hữu gọi getMessages() để xem tin nhắn

2.4 Thêm thành viên vào nhóm

Admin gọi addMember(user, userPublicKey, encryptedGroupPrivateKeyByMem)

Người dùng được thêm vào members mapping

Thành viên có thể gửi tin nhắn trong nhóm

2.5 Nhắn tin trong nhóm

Thành viên gọi sendMessage(encryptedMessage)

Tin nhắn được lưu vào messages

Thành viên khác gọi getMessages() để xem tin nhắn

3. Các Hàm Chính

3.1 Factory Contract

registerUser(string publicKey, string encryptedPrivateKey): Đăng ký người dùng

createGroup(string groupPublicKey, string encryptedGroupPrivateKey): Tạo nhóm

getUserContract(address user): Lấy hợp đồng người dùng

getGroupContract(uint256 groupId): Lấy hợp đồng nhóm

3.2 UserContract

sendMessage(string encryptedMessage): Gửi tin nhắn

getMessages(): Lấy danh sách tin nhắn

getEncryptedPrivateKey(): Lấy khóa riêng

markMessageAsRead(uint index): Đánh dấu tin nhắn đã đọc

3.3 GroupChat

addMember(address user, string userPublicKey, string encryptedGroupPrivateKeyByMem): Thêm thành viên

sendMessage(string encryptedMessage): Gửi tin nhắn nhóm

getMessages(): Xem tin nhắn nhóm

getEncryptedGroupPrivateKey(): Lấy khóa riêng của nhóm

4. Bảo Mật & Lưu Ý

Các tin nhắn và khóa riêng được mã hóa trước khi gửi lên blockchain.

Chỉ admin có thể thêm thành viên và xem khóa riêng của nhóm.

Chỉ chủ hợp đồng UserContract mới có thể xem tin nhắn cá nhân.
