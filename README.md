# Pacman-Project
This project is my solutions of Berkeley Pacman solution

## Problem Search

### Q1: DFS:

    Đầu tiên em  khai báo sử dụng Stack để duyệt đồ thị như trong môn câu trúc dữ liệu.
    Stack dùng để lưu vị trí và đường đi của một trạng thái.
    Thêm 1 list để lưu các action trả về cho pacman biết đường di chuyển.
    Một list để kiểm tra xem pacman đã đi qua vị trí này chưa

    Sử dụng hàm getStartState() ở search.py để lấy trạng thái khởi đầu ( là một tọa độ). Kiểm tra vị trí này liệu 
    nó phải kết thúc chưa bằng hàm ísGoalState().
    

    Nếu đúng trả về list các action còn không ta bắt đầu duyệt.

    Đưa trạng thái và các action cho đến hiện tại vào stack.

    Sử dụng 1 vòng lặp làm các động tác sau:

        +)Pop giá trị đầu tiên gồm vị trí và các action. Kiểm tra vị trí hiện tại có phải đích không? 
        Nếu đúng return các đường đã đi.

        +)Nếu không đánh dấu chỗ là này visited bằng cách thêm vị trí chỗ này vào list visited 
        sau đó sử dụng hàm getSuccessors() để lấy tất cả các đường đi có thể đi tiếp theo của 
        Pacman bao gồm tọa độ, hướng đi, chi phí di chuyển.

        +)Kiểm tra mọi đường đó, nếu cái nào chưa được thăm thì thêm action nó sẽ thực hiện rồi 
        ném vào stack.

        +)Như vậy cứ khi nào còn đường đi, trạng thái các đường có thể đi đó được lưu ở trong 
        Stack chờ lượt lấy ra để rồi lại đi tiếp cho đến khi không còn đường nữa.

        +)Vòng lặp dừng khi Stack rỗng 

    Nếu thoát ra khỏi vòng lặp tức đã đi hết những vị trí có thể nhưng vẫn không đến được đích vậy ta
    trả lại một list action rỗng.

### Q2: BFS
    Về cách giải ta làm y như cách duyệt DFS chỉ khác ở chỗ thay vì dùng Stack thì ta dùng Queue để 
    lưu những đỉnh   sẽ duyệt (vì Queue là cấu trúc LILO) nên khi Pop 1 Succesor ra 
    khỏi hàng đợi nó là sẽ Node ngay trước đó. Sau khi duyệt hết Node liên thông thì 
    mới duyêt sâu hơn xuống dưới. 
    
### Q3: UCS
    Để giải quyết bài này em sử dụng hàng đợi ưu tiên. Trong hàng đợi sẽ chứa 1 tuple có vị trí, đường
    đã đi để đến đó và chi phí để đến đó, cùng với đó là 1 biến ưu tiên (là giá trị của chi phí đi
    đến đó hay g(x)).

    g(x) của StartState gán giá trị 0.

    Đến đây cách làm giống như 2 bài trên:

        +)Pop giá trị đầu tiên gồm vị trí, các action và cost. Kiểm tra vị trí hiện tại có phải đích không? 
        Nếu đúng trả lại list đường đã đi.
        
        +)Nếu không đánh dấu chỗ là này visited bằng cách thêm vị trí chỗ này vào list visited 
        sau đó sử dụng hàm getSuccessors() để lấy tất cả các đường đi có thể đi tiếp theo của 
        Pacman bao gồm tọa độ, hướng đi, chi phí di chuyển.

        +)Kiểm tra mọi đường đó, nếu cái nào chưa được thăm thì thêm vị trí, đường đi tiếp rồi chi
        phí đến đó (bằng cách lấy chi phí đi đến vị trí trước cộng với chi phí mới) vào hàng đợi ưu tiên.

        +)Như vậy cứ khi nào còn đường đi, trạng thái các đường có thể đi đó được lưu ở trong 
        hàng đợi chờ lượt lấy ra để rồi lại đi tiếp cho đến khi không còn đường nữa.

        +)Vòng lặp dừng khi Queue rỗng.

### Q4: Astar
    Lúc này làm tương tự bài 3 ngoại trừ biến ưu tiên được truyền khác. Lúc này ngoại trừ chi phí đi đến 
    điểm đó từ vị trí khởi đầu ta cần cộng thêm giá trị hàm "kinh nghiệm" - là một hàm ước tính chi phí 
    từ trạng thái hiện tại đến đích của bài toán. Hàm này được cung cấp sẵn trong search.py.

### Q5: Finding All the Corners
    Ở bài này ta phải định nghĩa getStartState, isGoalState và getSuccessors để sao cho khi tìm kiếm tất
    cả các góc với thuật toán bfs bằng searchAgent này sẽ thu được kết quả đúng. Vì đề yêu cầu phải đi
    qua 4 góc được lưu tọa độ trong self.coners ta tạo 1 mảng đánh dấu góc đã được đi qua chưa bằng True,
    False rồi trả về ở getStartState. Điều kiện dừng là khi mảng trên đều mang giá trị true (đã đi qua).
    Hàm getSuccessors trả về mảng gồm state, action và cost trong đó state[0] là tọa độ, state[1] là
    mảng đánh dấu góc đã đi qua khi pacman ở tọa đô state[0] và thực hiện những action tương ứng.
    Ta chỉ cần kiểm qua Pacman có đi được trong 4 hướng di chuyển không, di chuyển được thì có đi qua
    góc không, nếu có thì thay đổi mảng đánh dấu tại góc đó thành true. Rồi đẩy vào mảng successors. 

### Q6: Corners Problem: Heuristic
    Hàm cornersHeuristic cần trả về giá trị là một số xác định. Giá trị đó là giá trị "kinh nghiệm",
    ước lượng chi phí từ điểm hiện tại đi đến đích. Giá trị này dùng khi thuật toán tìm kiếm là A*.
    Ta chỉ cần tạo 1 mảng lưu khoảng cách manhattan từ ví trí hiện tại đến những góc chưa đi qua.
    Rồi trả về giá trị lớn nhất của mảng để ước lượng.
### Q7: Eating All The Dots
    Giống như bài trước chỉ cần trả về 1 giá trị cụ thể. Và đích trong vài này là ăn hết đồ ăn trong
    mê cung. Nếu dùng manhattan để ước lượng thì điểm sẽ không tối đa do pacman rẽ quá nhiều. Vì vậy
    em dùng hàm mazeDistance để do khoảng cách giữa 2 điểm trong trạng thái bất kì của mê cung. Lưu 
    chúng lại thàng mảng rồi trả về giá trị lớn nhất.
### Q8: Suboptimal Search
    Do A* trong một số trường hợp cũng không thể cho chúng ta kết quả tối ưu nên có thể dùng tư duy
    tham lam để ăn hết thức ăn, đó là ăn thức ăn gần mình nhất. Vì cần thiết kế một cách duyệt luôn
    đi đến điểm có thức ăn gần nhất trước. Tuy nhiên không phải lúc nào cũng tìm được đường ngắn
    nhất tring suốt mê cung cho nên ta có thể ước lượng. Dùng cách duyệt bằng hàng đợi ưu tiên với
    tham số ưu tiên là khoảng cách manhatan từ điểm hiện tại đến các điểm cần đến để khi pop ra ta
    lấy được điểm có khoảng cách manhatan bé nhất.