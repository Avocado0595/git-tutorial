
# Git level tiểu học

  

*Bài này hướng dẫn một vài bước cơ bản cho các bạn có thể sử dụng được git, up project của mình lên github để chia sẻ cho bạn bè hoặc chỉ lưu trữ.*

  
  

## Git ở local (*là git nằm trên máy của mình ấy*)

#### 1. Cài đặt

Giờ muốn dùng git thì đầu tiên phải tải git cái đã, tải ở đây nè: [https://git-scm.com/](https://git-scm.com/) .

Tải xong rồi cài vào máy nha, cứ next thôi là được rồi. Cài đặt xong rồi thì kiểm tra coi đã được chưa bằng cách mở cmd gõ: ```git --version```

  

Thấy hiện như này là oke con dê:

  

![git version](/lecture01/gitversion.png)

  

#### 2. Các lệnh cơ bản

Giả sử mình có 1 file index.html trong thư mục demo-git như sau:

  

![git version](/lecture01/folder.png)

  

Chúng ta mở terminal lên:

  

Có 2 cách:

* Cách 1: nếu bạn dùng Visual Studio Code thì ấn ```Ctr + ` ``` , (hoặc bất kỳ ide nào có tích hợp terminal thì cứ bật lên thui)

![vsc terminal](/lecture01/vsc-terminal.png)

* Cách 2: mở cmd (hoặc powershell) tại thư mục chứa code tương ứng

  

(tip: bạn mở thư mục chứa code:

![cmd1](/lecture01/cmd1.png)

  

gõ vào ô đường dẫn ```cmd``` (hoặc ```powershell```), xong enter:

![cmd2](/lecture01/cmd2.png)

tada =))) cmd hiện ra ngay đúng thư mục của mình (*nếu mọi người đã quen với các câu lệnh trên cmd thì có thể dùng ```cd <tên folder>``` để di chuyển đến thư mục mình cần!*)

  

![cmd3](/lecture01/cmd3.png)

Giờ sẽ là dòng lệnh đầu tiên: ```git init```

  ![git init](/lecture01/git_init.png)

*Có ý nghĩa là khởi tạo 1 git repository local ngay trong thư mục (ý là phải khởi tạo tui đi thì tui mới chạy được chứ!)*
Lúc này nếu bạn kiểm tra trong thư mục, bật hiển thị file ẩn thì sẽ thấy có 1 file ```.git```

Tiếp theo là: ```git add .```

![git add](/lecture01/git_add.png)

Có nghĩa là thêm những file mình cần đưa vào git. Dấu “.” là thêm tất cả các file, nếu muốn thêm file nào cần thôi thì dùng ```git add <tên file>``` . (Các bạn có thể bỏ qua các file hoặc thư mục không cần commit bằng cách tạo file ```.gitignore```  - mình sẽ giải thích cụ thể hơn ở bài sau)

Dùng lệnh ```git status``` để kiểm tra xem đã add đúng chưa nha

![git status](/lecture01/git_status.png)

Sau khi add thì mình còn 1 bước nữa (tạm gọi là xác nhận những thay đổi) với lệnh: ```git commit -m “<ghi chú nội dung>” ```

Nhớ là có dấu ngoặc kép “” trong phần ghi chú nha, ví dụ: ```git commit -m “first commit”```

![git commit](/lecture01/git_commit.png)

Đó, vậy là xong òi. Mình đã lưu dc 1 commit đầu tiên òi. Để chắc cú thì mình phải kiểm tra lại đã.
Kiểm tra commit: ```git log```

![git log](/lecture01/git_log.png)

Chỗ này sẽ hiện ra id commit (do git tự tạo – sau này sẽ có lúc cần đến), người commit (author), thời gian commit, và ghi chú commit.

Tén tèn! Vậy là đã lưu dc rồi, giờ tới phần tiếp theo là up code lên github.

## Git Remote (*nơi lưu trữ code online*)

Để up code lên github thì ... phải đăng nhập github đã: [https://github.com/](https://github.com/) *(ai chưa có tài khoản thì nhớ đăng ký nhé)*

Sau khi đăng nhập thành công, chúng ta cùng tạo 1 repository (*từ này dịch tiếng việt nghĩa là kho - ý là cái kho để lưu và quản lý code cho chúng ta ấy!*).

Click nút New:

![new repo](/lecture01/new_repo.png)

Mọi người sẽ thấy 1 giao diện như thế này:

![create repo](/lecture01/create_repo.png)

Điền vào các thông tin cần thiết:

 - Repository name: tên repo
 - Description: mô tả repo này
 - Public (mọi người sẽ thấy được code của bạn nếu có link)  - Private (chỉ bạn , và
   những người bạn cho phép mới thấy được)
 - Khởi tạo các file: ```README.md, .gitignore, license```

(lưu ý: mục có * là bắt buột nhé)

Click Create Repository để tạo, chúng ta sẽ có được giao diện như sau:

![git log](/lecture01/repo_first_view.png)

Ở đây, chúng ta sẽ thấy hướng dẫn để push (đẩy code) từ git local ban đầu lên git remote trên github. (có 1 hướng dẫn phía trên là tạo mới nữa, nhưng do chúng ta đã tạo ban đầu rồi thì không cần tạo nữa đâu nha)

Giờ thì mọi người có thể mở terminal và làm theo các bước hướng dẫn là được:
```git remote add origin <link repo>``` - thêm dường dẫn remote vào git local

```git branch -M main``` - tạo 1 nhánh main (nhánh chính trong repo)

```git push -u origin main``` - push code ở nhánh main lên remote link

Khi push thành công, chúng ta sẽ được như thế này:

![git push origin](/lecture01/git_push_origin.png)

và trên github là như này:

![git push](/lecture01/push_github.png)

Tada =))) Vậy là đã up được code lên github òi! :3 Quá là xịn xò, giờ chỉ cần gửi link là có thể chia sẻ code với mn mà không cần phải gửi 1 cục code nữa :3.
Link chỗ này nè (nhớ chỉnh link https nha :3) :

![link git](/lecture01/link_github.png)

Nhưng mà ứng dụng của git không phải chỉ đơn giản là thế ! Ở bài viết sau mình sẽ giới thiệu chi tiết hơn về chức năng, cách hoạt động của git nhé ! Mọi người đọc thấy uki thì cho mình 1 sao github nhé <3 !!!!


*Có thể bạn biết rồi: trang bạn đang đọc cũng được mình up lên github theo y như các bước trong hướng dẫn vậy :3*
