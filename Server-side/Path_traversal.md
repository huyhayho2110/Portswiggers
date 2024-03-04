# 1. What is path traversal?

Path traversal (Truyền tải đường dẫn) is also known as directory traversal. These vulnerabilities(những lổ hổng) enable an attacker to read arbitrary (tùy ý) files on the server that is running an aplication. This might include:

* Application code and data.
* Credentials (Thông tin xác thực) for back-end systems.
* Sensitive (nhạy cảm) operating system files.

In some cases, an attacker might be able to write to arbitrary files on the server, allowing them to modify (biến đổi) application data or behavior, and ultimately take full control of server.

---
# 2. Reading arbitrary files via path traversal

Imagine a shopping application that displays images of items for sale. This might load an images using the following HTML:

* <img src="/loadImage?filename=218.png"> 

The **loadImage** URL takes a **filename** 