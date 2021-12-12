## Các lệnh "undo", giải quyết conflict trong git:

*Lần trước chúng ta đã tìm hiểu về việc tạo branch và merge branch vào, và mình cũng đã đề cập đến việc 2 branch cùng chỉnh sửa 1 file và cùng commit vào thì sẽ gây ra conflict. Vậy vấn đề này sẽ được giải quyết như thế nào?*

### Trước khi giải quyết vấn đề trên chúng ta cùng tìm hiểu 1 vài lệnh "undo" trong git nhé!
1. ```git reset``` : dùng để "unstaged" file vừa add (chưa commit) trong lệnh ```git add <file>```.
2. ```git checkout <id commit>```: dùng để back về commit có id tương ứng (cách tạm thời)
    
    Ví dụ:
    mình dùng ```git log``` để kiểm tra lịch sử commit
    ![](/lecture03/git-checkout-commit-1.png)
    Sau đó mình muốn quai lại commit có id bf712f66fd1b8b63b1bd26f9ec9f3f4b8ae179cb thì dùng lệnh:
    ```git checkout bf712f66fd1b8b63b1bd26f9ec9f3f4b8ae179cb```
    
    => quá trình chỗ này cũng giống như tạo 1 branch (tạm thời) mới tại commit này (mọi người có thể kiểm tra lại sau khi checkout bằng lệnh: ```git branch``` sẽ thấy có 1 branch main và 1 branch HEAD)
    
    Lúc này HEAD sẽ trỏ vào id mà mình vừa checkout - và nội dung code cũng thay đổi ứng với lúc tạo ra commit đó.
    ![](/lecture03/git-checkout-commit-2.png)
    Mọi người có những lựa chọn sau:

      - Trở lại trạng thái ban đầu dùng: ```git checkout main``` hoặc ```git switch -```
      - Tạo 1 branch mới tại commit này để tiếp tục code (từ commit này): ```git switch -c <new-branch-name>```
3. ```git reset <mode> <commit id>```: 
    + ```git reset --soft <commit id>```: code vẫn giữ nguyên, nhưng nội dung commit đã back về commit id tương ứng, và những commit ở giữa commit đó và HEAD sẽ chuyển về trạng thái modified (xem lại bài 02 về trạng thái này nhé :3 )
    + ```git reset --hard <commit id>```: xóa bỏ hoàn toàn commit id tương ứng. (giống delete permanently, không thể khôi phục lại được nhé @@)
    + Mọi người có thể tham khảo thêm các option khác tại: https://git-scm.com/docs/git-reset
4. ```git revert <commit id>```: tạo 1 commit mới để chỉnh sửa commit cũ. Lệnh này đưa trạng thái của 1 commit cũ lên đầu để chỉnh sửa và commit lại (thành 1 commit mới). Lưu ý với ```git revert``` sẽ có thể tạo nên conflict nếu bạn sửa 1 commit cũ bị trùng với những commit mới hơn, nên hạn chế việc revert này !
5. Conflict khi push code:
    Ví dụ mình có 1 file index.html, do 2 user 1 và user 2 cùng phát triển, cả 2 vô tình add code vào cùng 1 dòng tại local:
    ![ảnh conflict1](/lecture03/conflict-1.png)
    sau đó cùng push lên git remote (github), thì người push sau sẽ bị lỗi như sau:
    ![ảnh conflict2](/lecture03/conflict-2.png)

    Vấn đề này được giải quyết như sau:
    + Dùng ```git pull``` để pull code từ remote về, lúc này chúng ta sẽ thấy chỗ bị conflict
    ![ảnh conflict3](/lecture03/conflict-3.png)
    + Sau đó là vấn đề teamwork nhé (mọi người thảo luận xem thống nhất code như thế nào? :3) rồi giữ phần thống nhất, push code lên lại là được. Khi thống nhất code thì các bên local cần pull lại code trước khi push mới nhé!

6. Một số lệnh bổ sung trong git
   
   + Khi có 1 thay đổi nhỏ mà không muốn commit mới (chỉ cần gộp chung với commit cũ): ```git commit --amend```, lúc này 1 editor hiện ra (nó là Vim mà lúc mình chọn trong cài đặt ấy, hoặc là editor khác tùy lúc cài đặt ban đầu mà thường default là Vim, trong Ubuntu thì là Nano nhé - Nano thì có hướng dẫn hiện ngay trên editor). Nếu là VIM:
     + Bấm ```a``` để có thể chỉnh sửa message của commit.
     + Bấm ```ESC``` để thoát chế độ INSERT (chú ý góc dưới bên trái).
     + Sau đó gõ: ```:wq``` để lưu và thoát.
   ![ảnh commit amend](/lecture03/commit-amend.png)
   + ```git merge --no-ff <branch-name>```: như mọi người đã biết ở bài trước, để merge 1 branch A vào 1 branch B, thì tại branch B chúng ta dùng ```git merge A``` => lúc này các commit ở branch A sẽ được đưa về đầu branch B, cách thức này gọi là fast-forward: merge nhanh và gom nhánh lại. Các này giúp cho chúng ta có 1 cây git trông *thẳng hơn* và *gọn hơn*. @.@
   ![ảnh merge ff](/lecture03/merge-ff.png)
   
        Ngoài cách trên, chúng ta có thêm 1 cách merge nữa là ```git merge --no-ff <branch-name>```, cách này thay vì gom thẳng thì merge sẽ tạo 1 commit merge, và giữ lại đường merge như hình, cách thức này giúp chúng ta kiểm tra lại được commit được tạo và merge từ branch nào.
   ![ảnh merge no-ff](/lecture03/merge-noff.png)


   + Tạo branch từ 1 commit bất kỳ ```git branch <tên branch mới> <id của commit cũ>```. Nếu tạo nhánh kiểu này thì khi merge vào master sẽ tạo thêm 1 commit merge rồi mới merge vào branch.
   ![ảnh old commit branch](/lecture03/cricle-branch-merge.png)
   Như ảnh trên này, mình tạo 1 branch newfeature từ commit C2 sau đó merge tại main C6. Nhìn hình này thì có vẻ giống như merge no-fast-forward nhỉ @.@.
7. Một số lệnh rút gọn
   + Commit và muốn bỏ qua bước ```git add .``` : ```git commit -a "message"``` - commit theo cách này chỉ áp dụng với thay đổi trong file đã add hoặc commit trước đó nhé, file mới tạo ra sẽ không vào commit này.
   + Tạo branch và checkout ngay lúc tạo: ```git checkout -b <tên branch>```
   
