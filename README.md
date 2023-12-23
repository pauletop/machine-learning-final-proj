# Đây là bài cuối kỳ của môn học Nhập môn Học máy
# Phần tìm hiểu - đây là một bản tóm tắt nếu muốn đọc chi tiết hơn thì xem file [report.pdf](./52100920_NguyenMinhPhu.docx)
## Optimizer
### Optimizer là gì?
Nói một cách ngắn gọn optimizer hay còn được gọi là thuật toán tối ưu hóa là một thuật toán được sử dụng để tối ưu hàm mục tiêu. Trong machine learning, hàm mục tiêu thường là hàm mất mát (loss function) và mục tiêu của chúng ta là tìm ra bộ tham số sao cho hàm mất mát đạt giá trị nhỏ nhất. Ví dụ như trong bài toán hồi quy tuyến tính, hàm mất mát là hàm bình phương sai số (mean square error) và mục tiêu của chúng ta là tìm ra bộ tham số sao cho hàm bình phương sai số đạt giá trị nhỏ nhất. Trong bài viết này, chúng ta sẽ tìm hiểu về các thuật toán tối ưu hóa trong machine learning.
### Các thuật toán tối ưu hóa
#### Gradient Descent
Đây là thuật toán tối ưu hóa đơn giản nhất trong học máy. Nó thường được sử dụng để tìm giá trị nhỏ nhất của một hàm số. Ý tưởng của thuật toán này là ta sẽ khởi tạo một điểm bất kỳ trên đồ thị của hàm số và sau đó ta sẽ di chuyển điểm đó theo hướng ngược với độ dốc của hàm số. Độ dốc của hàm số được tính bằng đạo hàm của hàm số tại điểm đó. Nhưng không phải lúc nào đạo hàm của hàm số cũng có thể tính được. Vì vậy, ta sẽ xấp xỉ đạo hàm của hàm số bằng cách lấy đạo hàm của hàm số tại một điểm gần điểm đó. Điểm đó được gọi là điểm lân cận. Điểm lân cận này được tính bằng cách cộng điểm đó với đạo hàm của hàm số tại điểm đó nhân với một hệ số học tập (learning rate). Hệ số học tập này quyết định độ lớn của bước nhảy mà điểm đó sẽ di chuyển. Nếu hệ số học tập quá lớn thì điểm đó sẽ bị nhảy quá xa so với điểm nhỏ nhất của hàm số. Ngược lại, nếu hệ số học tập quá nhỏ thì thuật toán sẽ chạy rất lâu để tìm được điểm nhỏ nhất của hàm số. Vì vậy, hệ số học tập cần được chọn sao cho phù hợp. Đây là công thức của thuật toán Gradient Descent:
$$
x_{n+1} = x_n - \alpha \nabla f(x_n)
$$
Trong đó:
- $x_n$ là điểm hiện tại
- $x_{n+1}$ là điểm tiếp theo
- $\alpha$ là hệ số học tập
- $\nabla f(x_n)$ là đạo hàm của hàm số tại điểm $x_n$
Một cách tổng quát, với thuật toán này, Gradient Descent sẽ cố gắng thực hiện tìm cực tiểu của hàm số $f(x)$ bằng cách di chuyển điểm $x$ theo hướng ngược với độ dốc của hàm số $f(x)$. Tuy nhiên với một số hàm số, Gradient Descent có thể không tìm được cực tiểu của hàm số mà chỉ tìm được điểm cực tiểu cục bộ của hàm số. Để khắc phục điều này, ta có thể sử dụng thuật toán được đề cập ở phần tiếp theo.
#### Stochastic Gradient Descent
Thuật toán Stochastic Gradient Descent (SGD) là một biến thể của thuật toán Gradient Descent. Ý tưởng của thuật toán này là thay vì sau mỗi epoch ta sẽ cập nhật tham số của mô hình dựa trên toàn bộ tập dữ liệu một lần thì với thuật toán SGD, với N điểm dữ liệu, ta sẽ cập nhật tham số của mô hình N lần. Với mỗi lần cập nhật tham số, ta sẽ lấy một điểm dữ liệu ngẫu nhiên trong tập dữ liệu và tính đạo hàm của hàm mất mát tại điểm đó. <br>
Như vậy, ở một khía cạnh nào đó, thì việc cập nhật trọng số một lần sẽ nhanh hơn so với việc cập nhật trọng số N lần. Tuy nhiên, với việc cập nhật trọng số N lần, ta sẽ có được một mô hình tốt hơn. Dễ thấy, nó sẽ giúp tốc độ hội tụ rất nhanh chỉ sau vài epoch, hơn là phải mất nhiều epoch để hội tụ như thuật toán Gradient Descent. <br>
Đây là công thức của thuật toán SGD:
$$
x_{n+1} = x_n - \alpha \nabla f(x_i)
$$
Trong đó:
- $x_n$ là điểm hiện tại
- $x_{n+1}$ là điểm tiếp theo
- $\alpha$ là hệ số học tập
- $\nabla f(x_i)$ là đạo hàm của hàm số tại điểm $x_i$
#### Momentum
Gradient Descent và SGD có một nhược điểm là chúng có thể bị mắc phải điểm cực tiểu cục bộ của hàm số. Để khắc phục điều này, ta có thể sử dụng thuật toán Momentum. Ý tưởng của thuật toán này là ta sẽ tính trung bình có trọng số của các gradient trước đó để cập nhật trọng số hiện tại. Như vậy, nếu ta gặp phải điểm cực tiểu cục bộ thì ta vẫn có thể vượt qua được điểm đó. <br>
Đây là công thức của thuật toán Momentum:
- Công thức cập nhật vận tốc:
$$
v_{t+1} = \gamma v_t + (1 - \gamma) \nabla f(x_t)
$$
- Công thức cập nhật trọng số:
$$
x_{t+1} = x_t - \alpha v_{t+1}
$$
Trong đó:
- $v_t$ là vận tốc tại thời điểm t
- $x_t$ là trọng số tại thời điểm t
- $\gamma$ là hệ số momentum
- $\alpha$ là hệ số học tập
- $\nabla f(x_t)$ là đạo hàm của hàm số tại điểm $x_t$
Hãy thử liên tưởng dưới góc độ vật lý. Nếu Gradient Descent là một quả cầu lăn xuống dốc thì Momentum là một quả cầu lăn xuống dốc với vận tốc ban đầu. Như vậy, Momentum sẽ giúp ta vượt qua được các điểm cực tiểu cục bộ của hàm số.
#### AdaGrad
Thuật toán AdaGrad là một thuật toán tối ưu hóa khác được sử dụng trong machine learning. Ý tưởng của thuật toán này là ta sẽ cập nhật hệ số học tập của từng trọng số trong mô hình. Như vậy, với các trọng số có đạo hàm lớn thì hệ số học tập sẽ nhỏ hơn và ngược lại. Điều này giúp cho thuật toán hội tụ nhanh hơn. <br>
Khi so sánh với các thuật toán phía trên, khi hệ số học tập là một hằng số trong suốt quá trình huấn luyện thì với thuật toán AdaGrad, hệ số học tập sẽ thay đổi theo thời gian. <br>
Cụ thể, AdaGrad sử dụng một ma trận $G$ để lưu trữ tổng bình phương của các gradient trước đó. Mỗi phần tử của ma trận $G$ sẽ được cập nhật sau mỗi lần cập nhật trọng số. <br>
Đây là công thức của thuật toán AdaGrad:
$$
G_{t+1} = G_t + (1 - \gamma) \nabla (f(x_t))^2
$$
$$
x_{t+1} = x_t - \frac{\alpha}{\sqrt{G_{t+1} + \epsilon}} \nabla f(x_t)
$$
Trong đó:
- $G_t$ là ma trận tổng bình phương của các gradient trước đó
- $x_t$ là trọng số tại thời điểm t
- $\gamma$ là hệ số momentum
- $\alpha$ là hệ số học tập
- $\nabla f(x_t)$ là đạo hàm của hàm số tại điểm $x_t$
- $\epsilon$ là một hằng số nhỏ để tránh trường hợp chia cho 0
#### RMSProp
Cũng tương tự như thuật toán AdaGrad, RMSProp cũng sử dụng một ma trận $G$ để lưu trữ tổng bình phương của các gradient trước đó. Tuy nhiên, RMSProp sẽ sử dụng một hệ số momentum để cập nhật ma trận $G$. <br>
Đây là công thức của thuật toán RMSProp:
$$
G_{t+1} = \gamma G_t + (1 - \gamma) \nabla (f(x_t))^2
$$
$$
x_{t+1} = x_t - \frac{\alpha}{\sqrt{G_{t+1} + \epsilon}} \nabla f(x_t)
$$
Trong đó:
- $G_t$ là ma trận tổng bình phương của các gradient trước đó
- $x_t$ là trọng số tại thời điểm t
- $\gamma$ là hệ số momentum
- $\alpha$ là hệ số học tập
- $\nabla f(x_t)$ là đạo hàm của hàm số tại điểm $x_t$
- $\epsilon$ là một hằng số nhỏ để tránh trường hợp chia cho 0
#### Adam
Qua các thuật toán đã được trình bày ở trên, ta có thể thấy rằng mỗi thuật toán đều có những ưu điểm và nhược điểm riêng. Cụ thể, với thuật toán RMSProp, nếu hàm số có nhiều điểm cực tiểu cục bộ thì thuật toán này có thể không tìm được điểm cực tiểu của hàm số. Ngược lại, với thuật toán Momentum, nếu hàm số có nhiều điểm cực tiểu cục bộ thì thuật toán này có thể tìm được điểm cực tiểu của hàm số. <br>
Vì vậy, Adam được ra đời để kết hợp những ưu điểm của các thuật toán trên. Adam sử dụng một ma trận $G$ để lưu trữ tổng bình phương của các gradient trước đó và sử dụng một hệ số momentum để cập nhật ma trận $G$. <br>
Đây là công thức của thuật toán Adam:
$$
v_{t+1} = \beta_1 v_t + (1 - \beta_1) \nabla f(x_t)
$$
$$
G_{t+1} = \beta_2 G_t + (1 - \beta_2) \nabla (f(x_t))^2
$$
$$
x_{t+1} = x_t - \frac{\alpha}{\sqrt{G_{t+1} + \epsilon}} v_{t+1}
$$
Trong đó:
- $v_t$ là vận tốc tại thời điểm t
- $G_t$ là ma trận tổng bình phương của các gradient trước đó
- $x_t$ là trọng số tại thời điểm t
- $\beta_1$, $\beta_2$ là hệ số momentum
- $\alpha$ là hệ số học tập
- $\nabla f(x_t)$ là đạo hàm của hàm số tại điểm $x_t$
- $\epsilon$ là một hằng số nhỏ để tránh trường hợp chia cho 0
#### So sánh các thuật toán tối ưu hóa
Tôi sử dụng bảng dưới đây để so sánh các thuật toán tối ưu hóa:
| Thuật toán | Ưu điểm | Nhược điểm |
| --- | --- | --- |
| Gradient Descent | Thuật toán đơn giản nhất <br> Cơ bản, dễ hiểu, ổn định | Có thể bị mắc phải điểm cực tiểu cục bộ của hàm số <br> Tốc độ hội tụ chậm, tốc độ huấn luyện chậm <br> Phụ thuộc nghiệm ban đầu, khó xử lý trên dữ liệu lớn. |
| Stochastic Gradient Descent | Tốc độ hội tụ nhanh hơn so với Gradient Descent <br> Khắc phục được nhược điểm khó xử lý trên dữ liệu lớn của Gradient Descent | Có thể bị mắc phải điểm cực tiểu cục bộ của hàm số <br> Chưa giải quyết được vấn đề về nghiệm ban đầu và hệ số học tập |
| Momentum | Có thể vượt qua được điểm cực tiểu cục bộ của hàm số bằng cách sử dụng <i> đà </i> Giải quyết được vấn đề chỉ dừng lại ở điểm cực tiểu cục bộ của hàm số | Thuật toán có thể bị mắc phải điểm cực tiểu cục bộ của hàm số <br> Vẫn mất nhiều thời gian dao động quanh đích đến khi hội tụ |
| AdaGrad | Có thể hội tụ nhanh hơn so với các thuật toán khác <br> Tự động điều chỉnh hệ số học tập | Tốc độ hội tụ chậm hơn so với các thuật toán khác <br> Tổng bình phương sẽ lớn dần theo thời gian dẫn đến việc hệ số học tập giảm dần và dẫn đến việc thuật toán không còn hoạt động (đóng băng) |
| RMSProp | Có thể hội tụ nhanh hơn so với các thuật toán khác <br> Tự động điều chỉnh hệ số học tập, là một phiên bản cải tiến của AdaGrad, giúp giảm thiểu việc đóng băng của hệ số học tập | Thuật toán có thể bị mắc phải điểm cực tiểu cục bộ của hàm số |
| Adam | Kết hợp được những ưu điểm của các thuật toán khác <br> Cho hiệu quả tốt nhất trong hầu hết các trường hợp | Cần cấu hình nhiều tham số <br> Chi phí tính toán cao hơn so với các thuật toán khác |
---
Nhìn chung, các thuật toán tối ưu hóa đều có những ưu điểm và nhược điểm riêng. Vì vậy, để có thể chọn được thuật toán tối ưu hóa phù hợp, ta cần phải thử nghiệm nhiều thuật toán khác nhau và chọn ra thuật toán tối ưu hóa cho kết quả tốt nhất. Tuy nhiên, Adam thể hiện được hiệu quả tốt nhất trong hầu hết các trường hợp. Vì vậy, Adam là thuật toán tối ưu hóa được sử dụng nhiều nhất trong machine learning.
## Continual Learning & Test Production
### Continual Learning
#### Continual Learning là gì?
Continual Learning là một lĩnh vực nghiên cứu trong machine learning. Ý tưởng của Continual Learning là ta sẽ huấn luyện một mô hình trên một tập dữ liệu và sau đó ta sẽ huấn luyện lại mô hình đó trên một tập dữ liệu mới. Mục tiêu là để mô hình học máy có thể thích ứng với sự thay đổi của dữ liệu. <br>
Điều này có ý nghĩa rất lớn trong thực tế. Ví dụ như khi ta huấn luyện một mô hình nhận diện chữ viết tay, ta sẽ huấn luyện mô hình đó trên một tập dữ liệu và sau đó ta sẽ huấn luyện lại mô hình đó trên một tập dữ liệu mới. Mục tiêu là để mô hình học máy có thể nhận diện được chữ viết tay của nhiều người khác nhau. Giúp mô hình luôn được cập nhật với dữ liệu mới và phản ánh chính xác nhất với thực tế. <br>
Continual Learning giúp giải quyết vấn đề "quên" (catastrophic forgetting) của mô hình học máy. Vấn đề "quên" là vấn đề mà khi ta huấn luyện lại mô hình học máy trên một tập dữ liệu mới thì mô hình học máy sẽ quên đi những gì đã học trước đó. Dựa trên việc cập nhật mô hình học máy theo thời gian khi tiếp xúc với dữ liệu mới, thay vì chỉ huấn luyện một lần duy nhất, Continual Learning giúp mô hình học máy có thể học được nhiều kiến thức khác nhau mà vẫn "nhớ" được những gì đã học trước đó. <br>
Các kỹ thuật Continual Learning có thể được chia thành 3 nhóm chính để giải quyết vấn đề "quên":
- <b>Regularization-based</b>: Các kỹ thuật này sẽ thêm một số ràng buộc vào mô hình học máy để giúp mô hình học máy có thể học được nhiều kiến thức khác nhau mà vẫn "nhớ" được những gì đã học trước đó. Ví dụ như Elastic Weight Consolidation (EWC), Learning without Forgetting (LwF), ...
- <b>Rehearsal-based</b>: Các kỹ thuật này sẽ lưu trữ một số dữ liệu đã được huấn luyện trước đó và sau đó sẽ kết hợp dữ liệu đó với dữ liệu mới để huấn luyện mô hình học máy. Ví dụ như Memory Replay, Data Distillation, ...
- <b>Dynamic architectures</b>: Các kỹ thuật này sẽ thay đổi cấu trúc của mô hình học máy để giúp mô hình học máy có thể học được nhiều kiến thức khác nhau mà vẫn "nhớ" được những gì đã học trước đó. Ví dụ như Progressive Neural Networks (PNN), ...
#### Các kỹ thuật Continual Learning
##### Elastic Weight Consolidation (EWC)
Elastic Weight Consolidation (EWC) là một kỹ thuật Continual Learning thuộc nhóm Regularization-based. Ý tưởng của kỹ thuật này là ta giả định rằng các tham số trong mạng nơ-ron có một mức độ quan trọng đối với các tác vụ đã học. Vì thế, khi học một tác vụ mới, ta sẽ cố gắng giữ nguyên các tham số quan trọng của các tác vụ đã học trước đó, mà chỉ cập nhật các tham số không quan trọng. <br>
#### Learning without Forgetting (LwF)
Learning without Forgetting (LwF) là một kỹ thuật Continual Learning thuộc nhóm Regularization-based. Ý tưởng của kỹ thuật này là ta sẽ cố gắng giữ nguyên các đầu ra của mô hình học máy khi học một tác vụ mới. <br>
#### Dropout
Dropout là một kỹ thuật Continual Learning thuộc nhóm Regularization-based. Ý tưởng của kỹ thuật này là ta sẽ tắt một số nơ-ron trong mạng nơ-ron khi huấn luyện mô hình học máy. <br>
#### Memory Replay
Memory Replay là một kỹ thuật Continual Learning thuộc nhóm Rehearsal-based. Ý tưởng của kỹ thuật này là ta sẽ lưu trữ một số dữ liệu đã được huấn luyện trước đó và sau đó sẽ kết hợp dữ liệu đó với dữ liệu mới để huấn luyện mô hình học máy. Cũng giống như việc ta học một bài học mới, ta sẽ lưu trữ lại những gì đã học trước đó và sau đó ta sẽ kết hợp những gì đã học trước đó với những gì ta học mới để có thể học bài học mới. <br>
#### Data Distillation
Data Distillation là một kỹ thuật Continual Learning thuộc nhóm Rehearsal-based. Ý tưởng của kỹ thuật này là ta sẽ lưu trữ một số dữ liệu đã được huấn luyện trước đó (memory buffer), đồng thời tạo ra các mô hình nhỏ gọn (student model) để huấn luyện trên các dữ liệu đã được huấn luyện trước đó. Sau đó, ta sẽ kết hợp các mô hình nhỏ gọn đó với mô hình học máy chính (teacher model) cùng vớI dữ liệu mới để huấn luyện mô hình học máy chính. <br>
#### Progressive Neural Networks (PNN)
Progressive Neural Networks (PNN) là một kỹ thuật Continual Learning thuộc nhóm Dynamic architectures. Ý tưởng của kỹ thuật này là ta sẽ thêm một số tầng ẩn vào mạng nơ-ron khi học một tác vụ mới. Trong khi đó, các tầng ẩn đã học được từ các tác vụ trước đó sẽ được giữ nguyên. <br>
#### Forgetron
Forgetron là một kỹ thuật Continual Learning thuộc nhóm Dynamic architectures. Ý tưởng của kỹ thuật này là ta sẽ thêm các nơ-ron vào mạng nơ-ron khi học một tác vụ mới. Trong khi đó, các nơ-ron đã học được từ các tác vụ trước đó sẽ được giữ nguyên, và các nơ-ron ít quan trọng sẽ bị loại bỏ. Quá trình này giúp giải phóng bộ nhớ và giảm độ phức tạp của mạng nơ-ron mà vẫn giữ được hiệu suất. <br>
### Test Production
#### Test Production là gì?
Test Production là một kỹ thuật được sử dụng trong machine learning. Quá trình này, là để kiểm tra mô hình học máy có thể hoạt động tốt trên dữ liệu mới hay không trước khi đưa mô hình học máy được triển khai vào thực tế. Mục tiêu là đảm bảo mô hình học máy có thể hoạt động tốt như mong đợi, tránh trường hợp mô hình học máy hoạt động không tốt trên dữ liệu mới và giúp phát hiện các lỗi mà không thể tìm thấy khi kiểm thử mô hình học máy trên dữ liệu huấn luyện. <br>
Quá trình thực hiện Test Production bao gồm các bước sau:
- <b> Chuẩn bị dữ liệu </b>: Bước này gồm các công việc nhỏ như Thu thập dữ liệu, Xử lý dữ liệu, Chia dữ liệu, ...
- <b> Xây dựng mô hình học máy </b>: Mô hình học máy được xây dựng dựa trên dữ liệu đã được chuẩn bị ở bước trước đó.
- <b> Kiểm tra mô hình học máy </b>: Mô hình học máy được kiểm tra trên dữ liệu mới. Nếu mô hình học máy hoạt động tốt trên dữ liệu mới thì mô hình học máy sẽ được triển khai vào thực tế. Ngược lại, nếu mô hình học máy hoạt động không tốt trên dữ liệu mới thì mô hình học máy sẽ được cải tiến và kiểm tra lại trên dữ liệu mới.
- <b> Đánh giá mô hình học máy </b>: Mô hình học máy được đánh giá dựa trên các độ đo (metrics) liên quan đến mô hình học máy. Ví dụ như độ chính xác (accuracy), độ phủ (recall), độ chính xác dương tính (precision), độ chính xác âm tính (negative precision), ...
Khi thực hiện test production, ta cần phải chú ý đến các vấn đề sau:
- <b> Dữ liệu mới </b>: Dữ liệu mới cần phải được chuẩn bị kỹ lưỡng. Nếu dữ liệu mới không tốt thì mô hình học máy sẽ không hoạt động tốt trên dữ liệu mới.
- <b> Mô hình học máy </b>: Mô hình học máy cần phải được chọn sao cho phù hợp với bài toán. Nếu mô hình học máy không phù hợp với bài toán thì mô hình học máy sẽ không hoạt động tốt trên dữ liệu mới.
- <b> Độ đo (metrics) </b>: Độ đo (metrics) cần phải được chọn sao cho phù hợp với bài toán. Nếu độ đo (metrics) không phù hợp với bài toán thì có thể dẫn đến đánh giá sai về mô hình học máy.
- <b> Thời gian </b>: Thời gian thực hiện test production cần phải được đảm bảo. Nếu thời gian thực hiện test production quá lâu thì có thể dẫn đến việc mô hình học máy không được triển khai vào thực tế đúng thời điểm.
#### Các nguyên tắc khi thực hiện Test Production
- <b> Tính toàn vẹn của dữ liệu </b>: Dữ liệu cần phải được thu thập và chuẩn hoá cẩn thận. Nếu dữ liệu không tốt thì việc kiểm tra mô hình học máy sẽ không có ý nghĩa.
- <b> Tính đại diện của dữ liệu </b>: Dữ liệu cần phải đại diện cho dữ liệu thực tế. Nếu dữ liệu không đại diện cho dữ liệu thực tế thì việc kiểm tra mô hình học máy sẽ không có ý nghĩa.
- <b> Tính thời gian thực của dữ liệu </b>: Dữ liệu cần phải được thu thập và chuẩn hoá trong thời gian thực. Nếu dữ liệu không được thu thập và cập nhật thường xuyên theo thời gian thực để đảm bảo mô hình phản ánh chính xác nhất với thực tế.
#### Lợi ích của Test Production:
- Giúp đảm bảo chất lượng của mô hình trong điều kiện thực tế.
- Kiểm tra và tăng độ chính xác và tin cậy của mô hình.
- Phát hiện các vấn đề tìm ẩn.
- Giảm thiểu rủi ro khi triển khai mô hình vào thực tế.
#### Thách thức của Test Production:
- Chi phí thực hiện test production cao.
- Khó khăn về dữ liệu.