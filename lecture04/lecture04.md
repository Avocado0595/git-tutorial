## rebase và cherry-pick

#### 1. ```git rebase``` thay gốc 1 branch:
 Ví dụ mình có 2 branch ở 2 thời điểm khác nhau là ```feature/new01``` và ```feature2/new01```:

![rebase-1](/lecture04/rebase-1.png)


 1.1 Giờ mình muốn dùng những commit của branch ```feature/new01``` gắn tiếp vào ```feature2/new01``` thì dùng lệnh:

   + ```git checkout feature/new01``` => chuyển về ```feature2/new01```.
    
  + ```git rebase feauture2/new01``` => lúc này ```feature/new01``` sẽ nối tiếp vào ```feauture2/new01```.
![rebase-2](/lecture04/rebase-2.png)

(*2 branch màu hồng ban đầu giờ đã gộp thành 1 nhánh thẳng màu xanh*)

1.2. Trường hợp thứ 2 là rebase branch đã được merge từ branch khác - như branch ```new-branch03```dưới đây:
![preserve-1](/lecture04/rebase-preserve.png)
   + ```git checkout new-branch03```
   + ```git rebase new-branch04 --preserve-merges``` (câu lệnh này đã bị deprecated, nếu không được mọi người có thể dùng ```git rebase new-branch04 --rebase-merges```).
   ![preserve-2](/lecture04/rebase-preserve-2.png)

   Lúc này chúng ta gắn dc ```new-branch03``` và branch của nó vào ```new-branch04```. Với branch có merge branch phụ như thế này mọi người nên dùng cách này nhé !
#### 2. squash (nén commit khi rebase)

  Bạn có quá nhiều commit trên 1 branch và muốn nén nó lại cho gọn? Hãy dùng:
   + ```git rebase -i```
   
![rebase-i-1](/lecture04/rebase-i-1.png)

   + Một editor hiện ra, chúng ta có thể chỉnh các commit về squash, mọi người vẫn còn nhớ cú pháp với editor này chứ =))

   Gõ ```A``` để edit 
   
   Dùng phím mũi tên để di chuyển đến nơi cần chỉnh sửa: mình sẽ di chuyển con trỏ đến dòng ```pick``` thứ 2 và chỉnh thành ```squash```. Tức là mình sẽ nén 2 commit này lại thành 1 commit ```add 05 1```. Còn những tùy chọn bên dưới mọi người có thể tham khảo thêm trên google nhé!

![rebase-i-2](/lecture04/rebase-i-2.png)

   Nhấn ```ESC``` để thoát chế độ insert.

   Nhập ```:wq``` để lưu và thoát.

![rebase-i-3](/lecture04/rebase-i-3.png)

   Bảng này hiện lại để chúng ta xem lại những thông tin đã thay đổi.

   Nhập ```:q``` để thoát.
  + Lúc này branch được rebase vào chỉ hiện 1 commit đã squash vào.
![rebase-i-4](/lecture04/rebase-i-4.png)



#### 3. ```git cherry-pick commit1 commit2 commit3``` add nhiều commit khác nhau trong 1 lần.

Nếu chúng ta có 1 branch chứa vài commit, nhưng giờ chúng ta chỉ muốn sử dụng 1 vài commit trong branch này chứ chưa muốn merge cả branch vào, thì chúng ta có thể dùng ```git cherry-pick```. Cùng xem qua 1 ví dụ dưới đây nhé:

Ở đây mình có branch ```new06``` với 2 commit là ``add 8`` và ``add 9``.

![cherry-1](/lecture04/cherry-1.png)

Giờ mình muốn dùng commit ``add 8`` này đưa vào master thì sẽ dùng lệnh:

   + ``git checkout master``: chuyển về branch master

   + ``git cherry-pick <id của commit add 8>``

Chúng ta sẽ copy được commit ``add 8`` này vào master.
![cherry-2](/lecture04/cherry-2.png)

Mọi người có thể dùng ``git cherry-pick commit1 commit2 commit3`` để copy nhiều commit cùng lúc.

Có thể bạn biết rồi: Hình các branch git có màu hồng, màu xanh là từ extension Git Graph trên Visual Studio Code nhé!