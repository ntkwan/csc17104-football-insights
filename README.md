# [CSC17104] Football insights - Final Project

## Mục lục

1. [Giới thiệu](#i-giới-thiệu)

2. [Thông tin nhóm](#ii-thông-tin-nhóm)

3. [Thông tin đồ án](#iii-thông-tin-đồ-án)

4. [Tham khảo](#iv-tham-khảo)

## I. Giới thiệu

Repository là nơi lưu trữ sản phẩm của quá trình thu thập, khám phá và phân tích bộ dữ liệu từ [Kaggle](https://www.kaggle.com/datasets/slehkyi/extended-football-stats-for-european-leagues-xg) của nhóm trong phạm vi môn Lập trình khoa học dữ liệu. Mục tiêu của nhóm nhằm khai thác các thông số từ bộ dữ liệu để phân tích chuyên sâu về từng trận đấu bóng đá trong phạm vi các giải đấu hàng đầu Châu Âu. Từ các thông số này, ta có thể khai thác được mối liên hệ của các thông số với phong độ thực tế của đội bóng, từ đó đưa ra được những kết luận về các yếu tố ảnh hưởng đến thành tích của đội bóng trong một mùa giải, nhằm đưa ra những định hướng đung đắn về chiến thuật và chiến lược cho đội bóng. Nhóm hi vọng từ những tri thức này có thể được sử dụng cho những mô hình huấn luyện khác nhau phục vụ cho việc nghiên cứu và phát triển bóng đá.

## II. Thông tin nhóm:

- **Lớp:** 22KHDL

  | MSSV     | Họ tên            |
  | -------- | ----------------- |
  | 22127180 | Nguyễn Phúc Khang |
  | 21127346 | Nguyễn Trung Quân |
  | 21127451 | Phan Thị Tường Vi |

## III. Thông tin đồ án:

### 0. Tổng quan

- Notebook `01_collecting_data.ipynb`: Quan sát hai bộ dữ liệu thu thập được và tổng hợp thông tin của cả hai bộ dữ liệu cho quá trình khám phá và phân tích.
- Notebook `02_exploring_data.ipynb`: Khám phá và tiền xử lý bộ dữ liệu để đặt vấn đề và phục vụ trả lời câu hỏi.
- Notebook `main.ipynb`: Bao gồm toàn bộ quá trình xử lý dữ liệu và trả lời 12 câu hỏi đã được biên soạn lại từ các notebook câu hỏi riêng của từng thành viên.

### 1. Thu thập dữ liệu (Collecting data)

**Tác giả:** [Sergi Lehkyi](https://www.kaggle.com/slehkyi)

**Nguồn:** Dữ liệu được lấy từ trang [understat](https://understat.com)

**Phương pháp thu thập dữ liệu:** Thu thập dữ liệu từng trận đấu bằng việc crawl thông tin từ trang web (BeautifulSoup) thành 2 file csv và tổng hợp kết quả vào một file dữ liệu thống nhất. Bộ dữ liệu trong thư mục `data` là những dữ liệu đã qua xử lý nhằm phù hợp với mục đích nghiên cứu của đồ án. Bộ dữ liệu trong thư mục `raw data` là bộ dữ liệu gốc của tác giả. Trong đó, có 2 tập tin dữ liệu csv có ý nghĩa như sau:

- `understat.com.csv`: gồm các thông tin tổng quát của các đội ở các mùa giải trong từng hệ thống giải đấu.
- `understat_per_game.csv`: gồm các thông tin và thông số chuyên sâu về từng trận đấu của đội đó ở các mùa giải trong từng hệ thống giải đấu.

**Chủ đề:** Bộ dữ liệu được tham khảo từ trang [Football Data: Expected Goals and Other Metrics - Kaggle](https://www.kaggle.com/datasets/slehkyi/extended-football-stats-for-european-leagues-xg). Dữ liệu cho phép phân tích chuyên sâu về từng trận đấu trong các giải đấu hàng đầu Châu Âu, từ các thông số, ta có thể khai thác được những yếu tố ít được quan tâm nhưng làm nên sự thành công của đội bóng và từ đó kết luận được chiến thuật và chiến lược đội bóng áp dụng cho mùa giải.

Bộ dữ liệu bao gồm các thông số tổng hợp sau một mùa giải của các đội bóng thuộc 6 giải đấu thuộc UEFA từ năm 2014 đến năm 2019 bao gồm: La Liga (Tây Ban Nha), EPL (Anh), Bundesliga (Đức), Serie A (Ý), Ligue 1 (Pháp), RFPL (Nga)

### 2. Khám phá dữ liệu (Exploring data & preprocess)

**Ý nghĩa của từng đặc trưng:** Bộ dữ liệu sẽ gồm các thông số cơ bản như: thứ hạng (position), team (tên đội), số trận đã chơi trong giải đấu (matches), số trận thắng - hòa - thua (wins, draws, loses), số bàn ghi được (GF), số bàn thủng lưới (GA), số điểm (points). Ngoài ra, bộ dữ liệu còn các thông số khác như:

- xG - bàn thắng kỳ vọng, thông số thể hiện chất lượng của cú dứt điểm được tạo ra bởi cầu thủ. Trong bộ dữ liệu này, bàn thắng kỳ vọng thể hiện số chất lượng các cú dứt điểm đến từ đội bóng.

- xG_diff - sai số bàn thắng kỳ vọng, thông số thể hiện số lượng bàn thắng thực tế so với bàn thắng kỳ vọng được tạo bởi đội bóng.

- npxG - bàn thắng kỳ vọng không bao gồm đá phạt trực tiếp (penalty) và phản lưới nhà (own goal).

- xGA - số bàn thua kỳ vọng nhận được, thông số thể hiện chất lượng các cú dứt điểm được tạo ra bởi đối thủ khi đối đầu với đội bóng.

- xGA_diff - sai số bàn thua kỳ vọng nhận được, thông số thể hiện số lượng bàn thua thực tế so với số bàn thua kỳ vọng nhận được.

- npxGA - số bàn thua kỳ vọng không bao gồm đá phạt trực tiếp (penalty) và phản lưới nhà (own goal).

- npxGD - sai số giữa bàn thắng và bàn thua kỳ vọng không bao gồm đá phạt trực tiếp (penalty) và phản lưới nhà (own goal).

- ppda_coef - số đường chuyền thành công trên hành động phòng thủ trên phần sân đối phương, thông số thể hiện khả năng kiểm soát bóng của đội trên phần sân đối phương. Thông số cũng thể hiện khả năng gây áp lực (phòng thủ) của đối phương lên đội trên phần sân của đối phương.

- oppda_coef - số đường chuyền thành công trên hành động phòng thủ trên phần sân nhà, thông số thể hiện khả năng kiểm soát bóng của đối phương trên phần sân của đội. Thông số cũng thể hiện khả năng gây áp lực (phòng thủ) của đội lên đối phương trên phần sân nhà của đội.

- deep - số đường chuyền thành công (không bao gồm tạt bóng) của đội trong khu vực 18,3m so với khung thành của đối phương (khu vực [Zone 17](https://www.researchgate.net/figure/The-pitch-of-play-divided-into-18-zones_fig2_336578142))

- deep_allowed - số đường chuyền thành công (không bao gồm tạt bóng) của đối phương trong khu vực 18,3m so với khung thành của đội (khu vực [Zone 17](https://www.researchgate.net/figure/The-pitch-of-play-divided-into-18-zones_fig2_336578142))

- xpts - số điểm kỳ vọng của đội

- xpts_diff - sai số giữa số điểm thực tế và số điểm kỳ vọng của đội

- ...

**Thông tin các bộ dữ liệu**: Nhóm thực hiện phân tích trên 2 bộ dữ liệu `understat.com.csv` (tổng quan) và bộ dữ liệu `understat_per_game.csv` (chi tiết từng trận đấu), tạm gọi hai bộ dữ liệu này là `overview` và `details`, các bộ chi tiết bao gồm:

- `overview`: 684 dòng và 24 cột
- `details`: 24580 dòng và 29 cột
- Cả hai bộ dữ liệu đều không có dòng bị trùng lặp
- Sau khi thực hiện quá trình tiền xử lý, ta sẽ được 2 file tiền xử lý là `understat.com_preprocess.csv` và `understat_per_game_preprocess.csv`

**Các câu hỏi khác:** Các câu hỏi liên quan tới quá trình khám phá dữ liệu đã được phân tích chi tiết trong file [`02_exploring_data.ipynb`](https://github.com/ntkwan/csc17104-football-insights/blob/main/02_exploring_data.ipynb).

### 3. Câu hỏi được đúc kết từ quá trình khai thác dữ liệu (Asking meaningful questions)

Bao gồm 12 câu hỏi khác nhau, cụ thể:

- _Câu 1: Tỷ lệ thắng của các trận đấu khi diễn ra trên sân nhà và trên sân khách qua từng mùa giải (năm) như thế nào? Điều này có chứng minh được lợi thế sân nhà không?_

- _Câu 2: Liệu một đội có số trận thắng cao, số trận thua ít thì có xếp hạng cao hơn không? Thống kê trung bình thắng-hòa-thua giữa các thứ hạng._

- _Câu 3: Đội bóng nào có hiệu suất tốt nhất trong mỗi giải đấu?_

- _Câu 4: Các chỉ số như `deep` và `deep_allowed` có mối quan hệ thế nào với thứ hạng cuối cùng?_

- _Câu 5: Mối quan hệ giữa số điểm thực tế (pts) và số điểm kỳ vọng (xpts) là gì? Top 5 đội bóng của năm gần đây nhất của mỗi giải đấu được kỳ vọng và họ thể hiện thế nào? Sự kỳ vọng (xpts) có ảnh hưởng đến thứ hạng cuối không?_

- _Câu 6: Số lượng performance được phân bố như thế nào?_

- _Câu 7: Những chỉ số `xG`, `xGA`, `npxG`, `npxGA` và `xpts` có tương quan thế nào với kết quả trận đấu (thắng, hòa, thua)?_

- _Câu 8: Có sự khác biệt đáng kể nào về hiệu suất (xG, xGA, pts) giữa các trận sân nhà và sân khách không?_

- _Câu 9: Các chỉ số `PPDA` có tương quan như thế nào với kết quả trận đấu?_

- _Câu 10: Điểm số của các đội bóng thay đổi như thế nào qua các mùa giải, từ đó thấy được sự cạnh tranh giữa các mùa giải ra sao?_

- _Câu 11: Dựa trên điểm số đội bóng qua các mùa giải, điểm của các đội trong các giải đấu vào những năm tiếp theo là như thế nào?_

- _Câu 12: Các đội bóng có số trận thắng cao có đặc điểm gì về số bàn thắng ghi được và số bàn thua?_

### 4. Phân công

- [Kế hoạch phân công của các thành viên](https://drive.google.com/drive/folders/1O996Bsyh-EuSL-F8hDH8_6lHPJuBrI-J?usp=drive_link)

## IV. Tham khảo

- [Gradient Boosting Classifier - scikitlearn docs](https://scikit-learn.org/1.5/modules/generated/sklearn.ensemble.GradientBoostingClassifier.html)
- [Explaining xG, PPDA, field tilt and how to use them - NY Times](https://www.nytimes.com/athletic/2730755/2021/07/28/the-athletics-football-analytics-glossary-explaining-xg-ppda-field-tilt-and-how-to-use-them/)
- [Matplotlib visualization tips that make plots speak for themselves - Alexandr Koryachko
  ](https://www.xomnia.com/post/matplotlib-visualization-tips-that-make-plots-speak-for-themselves/)
- [Visualization with Seaborn - Jake VanderPlas](https://jakevdp.github.io/PythonDataScienceHandbook/04.14-visualization-with-seaborn.html)
