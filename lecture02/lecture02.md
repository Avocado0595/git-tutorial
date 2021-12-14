
### Hiểu về git

(Bài viết được tham khảo và dịch từ trang https://git-scm.com/ và https://www.atlassian.com/git/tutorials/ )

+ *Vấn đề 1:*  Vào 1 ngày đẹp trời, bạn đang code và chợt thấy rằng đoạn code A này không dùng nữa, thôi thì xóa đi, oke thế là bạn xóa nó đi. Vài hôm sau bạn lại thấy rằng, đoạn code cũ này xài tốt hơn mà, rồi làm sao nhớ được đoạn đó nhỉ? Oh, lại phải ngồi suy nghĩ lại thôi :”>. Quả thật là mất thời gian.

+ *Vấn đề 2*: Khi làm project theo nhóm, bạn phải chia công việc ra cho các thành viên, và code theo đó cũng được chia nhỏ ra, vậy mỗi lần muốn test một chức năng nào có liên quan với nhau thì mọi người trong team phải gửi code cho nhau, copy về, gom lại và test. Cứ mỗi lần như thế code bắt đầu nhiều lên, có khi chồng chéo lên nhau… Và có thể bạn sẽ ngồi note lại những code này của ai, sửa lúc nào, có vấn đề gì hay không,... :">

Từ những vấn đề trên chúng ta có : Version control - Quản lý phiên bản.

#### Version control là gì?

Version control (quản lý phiên bản) là việc chúng ta kiểm soát mọi sự thay đổi trong code (các phiên bản của code) như: thêm mới, sửa code cũ, xóa file, thêm file mới,…. Việc quản lý này không những giúp chúng ta luôn nắm bắt được mọi sự thay đổi trong code, mà còn giúp chúng ta dễ dàng duy trì, sửa lỗi, nâng cấp dự án của mình  một cách rõ ràng, khoa học.

#### Git là một hệ thống quản lý phiên bản phân tán (Distributed Version Control System):

```A distributed version control system (DVCS) is a type of version control where the complete codebase — including its full version history — is mirrored on every developer's computer. It's abbreviated DVCS.```

Có  thể coi như là: Git = 1 phần mềm để quản lý phiên bản + Hỗ trợ các máy con có thể clone về tạo ra nhiều bản sao giống như nhau từ máy chủ.

#### Git hoạt động như thế nào

![git flow](/lecture02/gitflow.png)

(nguồn: [https://git-scm.com/book/en/v2/Getting-Started-What-is-Git%3F](https://git-scm.com/book/en/v2/Getting-Started-What-is-Git%3F))

+ **Working Directory**: là thư mục chứa code chúng ta cần quản lý bằng git.

+ Tại working directory này chúng ta gõ lệnh: ```git init```=> tạo ra **.git directory**
 (repository ở local) => các phiên bản của git sẽ lưu ở đây.

+ **Staging directory** : là 1 file nằm trong **.git directory** => chứa các thông tin sắp được commit vào repository.

+ Ứng với 3 vị trí là 3 trạng thái của code: **modified** (code thay đổi trong working directory), **staged** (code đưa lên staging) và **commited** (code đã commit vào .git directory).

+ Đường đi của code như sau:  Tại working directory nhập: ```git init``` => .git directory và staging directory được tạo ra => gõ ```git add .``` => những thay đổi trong code sẽ được đưa vào staging directory => nhập ```git commit -m “my-commit” ```=> code được commit vào .git directory

*Có 1 câu hỏi nhỏ là: **tại sao phải add vào staging trước khi commit ?** – theo như mình đọc được một ví dụ như thế này: git là 1 thợ chụp ảnh, đang gọi 1 nhóm người ra để chụp, git add vào staging là người chụp ảnh đang chỉnh vị trí mọi người cho vừa khung ảnh (anh ta sẽ xem qua trong máy ảnh), còn git commit là chụp bức ảnh đấy. Như vậy, việc add vào staging cho chúng ta 1 bước để xem lại những thay đổi trước khi quyết định commit những thay đổi đó. Và dĩ nhiên nếu chúng ta chụp ảnh lệch chúng ta vẫn có thể chụp lại – nhưng mà sẽ phiền và mất thời gian đấy. Tương tự việc chúng ta quên xem thay đổi ở staging thì chúng ta vẫn có cách restore lại commit => và đương nhiên là sẽ tốn công hơn việc review trước ở staging rồi :”> .*

* Review thay đổi ở staging bằng lệnh: ```git diff –-staged``` 
* Để giữ những file trong working directory nhưng không theo dõi nó bằng git, thì chúng ta tạo 1 file tên là ```.gitignore``` trong thư mục tương ứng, sau đó thêm tên file hoặc thư mục không muốn add vào file này, mỗi tên cách nhau 1 hàng nhé. Ví dụ:

![note](/lecture02/gitignore.png)

* Mỗi lần ```git add .``` thì git sẽ bỏ qua những tên file và thư mục trong ```.gitignore```

#### GitHub (ngoài github còn có gitlab và 1 số công cụ khác nữa)

Github là 1 nơi để lưu trữ repository online. Khi chúng ta dùng ```git push``` chính là việc đưa repository ở local lên Github (bao gồm toàn bộ code commit và lịch sử commit ở local luôn nha)

+ ```git clone```

Ngược lại với việc đẩy commit lên github là lấy toàn bộ repo có trên github về máy với lệnh:
```git clone <url github>```

Git clone được dùng khi chúng ta muốn copy lại toàn bộ 1 repo của người khác, hoặc của mình. Khi clone về thì repo này chứa các thông tin về code cũng như lịch sử commit và link remote của nơi mà mình clone về.

+ ```git pull```

Khi chúng ta làm việc trong 1 team, sẽ có 1 repo trên github dùng chung. Mỗi khi thêm code mới bạn B sẽ push lên repo này. Bạn A muốn kiểm tra code này chạy như thế nào thì dùng git pull để cập nhật code mới trên github về máy của mình. (dĩ nhiên là cả 2 điều có quyền truy cập và kết nối đến repo này nhé :”> )

### Tóm tắt 2 bài qua sơ đồ sau nhé

![note](/lecture02/github.svg)

Trong thực tế thì chúng ta không push thẳng code vào github như thế này, mà chúng ta sẽ tạo các nhánh riêng, gọi là branch.

***********

Đầu tiên chúng ta cần biết mỗi commit đi vào sẽ tương tự như thế này
![commit chain](/lecture02/git-commit-chain.png)

Các commit sẽ gắn với nhau thành 1 chuỗi liên tục (giống như linked-list). Mỗi commit mới sẽ trỏ vào đầu commit trước đó. Ở phần trước, trước khi push lên github chúng ta có 1 lệnh:
``git branch -m main``, chính là việc đánh dấu cho nhánh làm việc chính của chúng ta là main. Đây là nhánh chính, chỉ nên push những code đã kiểm tra kỹ vào nhánh này.

Những code thêm vào để test thì chúng ta có thể tạo ra các nhánh khác. Tạo một nhánh, dùng lệnh:  ```git branch future-plans```

Lệnh này sẽ tạo ra 1 branch mới tên là ```future-plans``` (tên nhánh có thể đặt bất kỳ). Mọi người có thể tham khảo cách đặt tên branch như bảng này:

<table>
  <thead>
    <tr>
      <th>Instance</th>
      <th>Branch</th>
      <th>Description, Instructions, Notes</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Stable</td>
      <td>stable</td>
      <td>nhận merge từ Working và Hotfixes (chứa code ổn định nhất)</td>
    </tr>
    <tr>
      <td>Working</td>
      <td>master</td>
      <td>nhận merge từ Features/Issues và Hotfixes (nhánh làm việc chính)</td>
    </tr>
    <tr>
      <td>Features/Issues</td>
      <td>topic-*</td>
      <td>nhánh được tách từ HEAD của Working (nhánh phát triển tính năng hoặc sửa lỗi)</td>
    </tr>
    <tr>
      <td>Hotfix</td>
      <td>hotfix-*</td>
      <td>nhánh được tách từ stable Stable (nhánh fix nhanh những lỗi phát sinh)</td>
    </tr>
  </tbody>
</table>

Nguồn: https://gist.github.com/digitaljhelms/4287848


![](/lecture02/git-branch-01.png)

Như trên hình, nhánh này được tạo ra rồi nhưng chúng ta vẫn còn ở nhánh main nha. Giờ chúng ta sẽ phải chuyển sang nhánh mới này để làm việc
```git checkout future-plans```

![](/lecture02/git-branch-02.png)

Chúng ta có thể kiểm tra các branch đang có và mình đang ở branch nào thì dùng lệnh:

```git branch```

Tại thời điểm checkout sang nhánh mới thì mọi code thêm, xóa, sửa mới vào chỉ tồn tại trên nhánh đang làm việc mà thôi, hoàn toàn không ảnh hưởng đến branch khác.
Giả sử tại nhanh future-plans này code bị lỗi thì chúng ta có thể dùng ```git checkout main``` để quay lại code ban đầu, và bắt đầu 1 nhánh khác để tiếp tục phát triển.

Sau khi đã phát triển 1 nhánh hoàn thiện, thì chúng ta cần gộp nhánh đã tách vào lại main để sử dụng.
+ Branch ở local:
 
	* Tại nhánh future-plans, kiểm tra các thay đổi đã commit chưa, nếu commit hết rồi thì ok nhé!
	* Quay lại nhánh main: ``git checkout main``
	* Gộp nhánh future-plans vào main: ``git merge future-plans``
	* (Nếu) muốn xóa branch không cần dùng nữa đi: ``git branch -d future-plans``
+ Branch trên remote:
	* Tại nhánh future-plans, kiểm tra các thay đổi đã commit chưa, nếu commit hết rồi thì ok nhé!
	* Cũng tại nhánh này push lên remote bằng lệnh: ``git push origin future-plans``
	* Đăng nhập github kiểm tra branch, chúng ta sẽ thấy có 1 branch mới.    
![](/lecture02/github-branch-1.png)

    * Vào phần Pull request (Tạm gọi là tạo 1 yêu cầu kiểm tra code mình muốn đưa vào), chọn ``New pull request`` 
	* Tại đây chọn nhánh cần merge vào nhánh main (base - nhánh chính) ![](/lecture02/github-branch-3.png) => chọn ``Create pull request``, xuất hiện các thông tin sắp merge, cùng phần code thay đổi phía dưới, chúng ta kiểm tra lại rồi chọn ``Create pull request`` nếu thấy ok!
	* Tại đây nếu code không có bị xung đột (conflict) thì sẽ chúng ta chọn ``Merge pull request`` ![](/lecture02/github-branch-4.png)
	* Merge thàng công sẽ được như ảnh ![](/lecture02/github-branch-5.png)Quay lại mục code chúng ta sẽ thấy các thay đổi đã được merge vào main.
  

Phần này mình đã giới thiệu vài bước cơ bản trong quá trình sử dụng branch. Sẽ có 1 vấn đề khi code cùng 1 team là chúng ta vô tình modified cùng 1 file, khi đó merge vào thì sẽ bị báo là CONFLICT! Chúng ta sẽ tìm hiểu vấn đề này ở bài sau nhé !

*Note: Trong quá trình push code lên github nếu ở phía github chúng ta có sử đổi trực tiếp trên đó thì push sẽ báo lỗi ``error: failed to push some refs to...``, và sẽ có ``hint: git pull`` . Lúc này chỉ cần làm theo gợi ý: ``git pull`` trước, rồi ``git push`` là được nhé!*


Mọi người thấy hữu ích hãy cho mình 1 sao, mọi sai sót, góp ý mọi người cứ thoải mái đóng góp cho mình ở phần Issues nhé ! Cảm ơn mọi người đã đọc! <3
