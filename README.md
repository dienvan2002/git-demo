# git-demo

- Demo workshop git

## 🛠️ Xử lý nhanh các tình huống Git thực tế

|   #   | Tình huống                                                | Cách xử lý chuẩn                                                                                                                                                                                             | Lưu ý quan trọng                                                                            |
| :---: | :-------------------------------------------------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------ |
| **1** | **Đã push commit lỗi lên nhánh chung (`main`/`develop`)** | `git revert <commit-hash>`<br>`git push origin develop`                                                                                                                                                      | Không dùng `reset --hard` + `push -f` làm hỏng lịch sử team.                                |
| **2** | **Bị từ chối `push` do đồng nghiệp đẩy code trước**       | `git pull --rebase origin <nhánh>`<br>`git push origin <nhánh>`                                                                                                                                              | Nếu gặp conflict: sửa file $\rightarrow$ `git add .` $\rightarrow$ `git rebase --continue`. |
| **3** | **Cần Force Push nhánh cá nhân sau khi Rebase**           | `git push --force-with-lease origin <nhánh>`                                                                                                                                                                 | Luôn dùng `--force-with-lease` thay cho `-f` để tránh ghi đè code mới trên remote.          |
| **4** | **Lỡ code & commit nhầm vào `main` (chưa push)**          | `git branch feat/<nhánh-mới>`<br>`git reset --hard HEAD~<số-commit>`<br>`git switch feat/<nhánh-mới>`                                                                                                        | Tạo nhánh mới trước để giữ code, rồi mới reset `main`.                                      |
| **5** | **Gộp nhiều commit vụn thành 1 commit trước khi tạo PR**  | `git rebase -i HEAD~<n>`                                                                                                                                                                                     | Giữ `pick` ở commit đầu, đổi các dòng dưới thành `squash` (`s`) rồi đặt lại message.        |
| **6** | **Lỡ `reset --hard` hoặc xóa nhầm nhánh mất code**        | `git reflog`<br>`git switch -c <nhánh-cứu> <hash-cũ>`                                                                                                                                                        | `reflog` lưu nhật ký di chuyển `HEAD` trong 30–90 ngày.                                     |
| **7** | **Lỡ đẩy nhầm `.env` / API Key / Mật khẩu**               | **1.** Revoke/Rotate key ngay lập tức.<br>**2.** Local: `git rm --cached .env`, thêm vào `.gitignore`, rồi `git commit --amend`.<br>**3.** Remote: dùng `git-filter-repo` hoặc BFG Repo-Cleaner xóa lịch sử. | Đổi key/mật khẩu là ưu tiên số 1 trước khi xử lý lịch sử Git.                               |

test
test merge --rebase
tesst
