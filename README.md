# Pacman-Project
This project is my solutions of Berkeley Pacman solution

## Problem Search

### Q1: DFS:

    Đầu tiên em  khai báo sử dụng Stack để duyệt đồ thị như trong môn câu trúc dữ liệu.
    Thêm 1 list để lưu các action trả về cho pacman biết đường di chuyển.
    Một list để kiểm tra xem pacman đã đi qua vị trí này chưa

    Sử dụng hàm getStartState() ở search.py để lấy trạng thái khởi đầu ( là một tọa độ). Kiểm tra vị trí này liệu nó phải kết thúc 
    chưa bằng hàm ísGoalState().

    Nếu đúng trả về list các action còn không ta bắt đầu duyệt.

    Đưa trạng thái và các action cho đến hiện tại vào stack.

    Sử dụng 1 vòng lặp làm các động tác sau:

        Pop giá trị đầu tiên gồm vị trí và các action. Kiểm tra vị trí hiện tại có phải đích không? Nếu đúng thêm action vừa lấy ra vào list rồi return.

        Nếu không sử dụng hàm getSuccessors() để lấy tất cả các đường đi có thể đi tiếp theo của Pacman bao gồm tọa độ, hướng đi, chi phí di chuyển.

        Kiểm tra mọi đường đó, nếu cái nào chưa được thăm thì thêm action nó sẽ thực hiện rồi ném vào stack.

        Như vậy cứ khi nào còn đường đi, trạng thái các đường có thể đi đó được lưu ở trong Stack chờ lượt lấy ra để rồi lại đi tiếp cho đến khi không còn đường nữa.

        Vòng lặp dừng khi Stack rỗng 

    Nếu thoát ra khỏi vòng lặp tức đã đi hết những vị trí có thể nhưng vẫn không đến được đích vậy ta trả lại một list action rỗng.

### Q2: BFS
    Về cách giải ta làm y như cách duyệt DFS chỉ khác ở chỗ thay vì dùng Stack thì ta dùng Queue để lưu những đỉnh sẽ duyệt (vì Queue là cấu trúc LILO) nên khi Pop 1 Succesor ra khỏi hàng đợi nó là sẽ Node liên thông với Node ngay trước đó. Sau khi duyệt hết Node liên thông thì mới duyêt sâu hơn xuống dưới. 
