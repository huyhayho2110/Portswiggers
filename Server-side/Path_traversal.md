# 1. What is path traversal?

Path traversal (Truyền tải đường dẫn) is also known as directory traversal. These vulnerabilities(những lổ hổng) enable an attacker to read arbitrary (tùy ý) files on the server that is running an aplication. This might include:

* Application code and data.
* Credentials (Thông tin xác thực) for back-end systems.
* Sensitive (nhạy cảm) operating system files.

In some cases, an attacker might be able to write to arbitrary files on the server, allowing them to modify (biến đổi) application data or behavior, and ultimately take full control of server.

--- 
# 2. Reading arbitrary files via path traversal

Imagine a shopping application that displays images of items for sale. This might load an images using the following HTML:

<code class="code-scrollable">&lt;img src="/loadImage?filename=218.png"&gt;</code> 

The <code class="code-scrollable">loadImage</code> URL takes a <code class="code-scrollable">filename</code> parameters (tham số) and returns the contents of the specified (chỉ định) file. The image files are stored on disk in the location <code class="code-scrollabel">/var/www/images/218.png</code>. To return an image, the application appends (thêm) the requested filename to this base directory and uses a filesystem API to read the contents of the file. In other words, the application reads from the following file path:

<code class="code-scrollable">/var/www/218.png</code> 

This application implements (dụng cụ) no defends against (chống lại) path traversal attacks. As a result, an attacker can request the following URL to retrieve (lấy lại) the <code class="code-scrollable">/etc/passwd</code> file from the server's filesystem:

<code class="code-scrollable">https://insecure-website.com/loadImage?filename=../../../etc/passwd</code>

This cause the application to read from the following file path:

<code class="code-scrollable">/var/www/images/../../../etc/paswwd</code>

The sequence <code>