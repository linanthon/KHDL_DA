# KHDL: ĐỒ ÁN CUỐI KÌ

Lấy cảm hứng từ bài toán dự đoán giá rượu, nếu dựa trên các thuộc tính thu thập được mà có thể dự đoán ra giá tiền thì chúng ta không cần có người định giá rượu nữa. Và đề tài của chúng tôi là dự đoán lương của các cầu thủ bóng rổ cho mùa tiếp theo dựa trên chỉ số của họ trong mùa này.

![alt text](https://github.com/linanthon/KHDL_DA/blob/master/Image_for_readme/basketball_wallpaper.jpg)

## Trang web

### Thông tin cầu thủ
Trước hết, chúng ta cần có thông tin của cầu thủ. Và trong đồ án này, chúng ta chỉ xét tất cả các trận đấu của họ trong 2018-2019 mà được đề cập trong trang này: https://www.basketball-reference.com/leagues/NBA_2019_per_game.html

![alt text](https://github.com/linanthon/KHDL_DA/blob/master/Image_for_readme/source_player.png)

Trong đó, các thuộc tính có ý nghĩa như sau:

  - Rk (Rank): Thứ hạng
  - Pos (Position): Vị trí
  - Age: Tuổi của cầu thủ tại thời điểm ngày 01 tháng 02 của mùa tương ứng    
  - Tm (Team): Đội    
  - G (Games): Số trận đấu tham gia    
  - GS (Games Started): Số trận đấu mà là người dắt bóng đầu tiên    
  - MP (Minutes Played Per Game): Thời gian chơi mỗi trận
  
Lưu ý, từ đây, các số liệu này là lấy trung bình của tất cả các trận mà cầu thủ đó tham gia:
  - FG (Field Goals Per Game): Số lượng bàn ghi mỗi trận
  - FGA (Field Goal Attempts Per Game): Số lần cố gắng ghi bàn mỗi trận (cố gắng tức là có thể có hoặc không ghi bàn)    
  - FG% (Field Goal Percentage): Tỉ lệ ghi bàn = FG / FGA * 100%
  - 3P (3-Point Field Goals Per Game): Số lượng bàn ghi mà là 3 điểm mỗi trận
  - 3PA (3-Point Field Goal Attempts Per Game): Số lân cố gắng ghi bàn 3 điểm mỗi trận
  - 3P% (FG% on 3-Pt FGAs.): Tỉ lệ ghi bàn 3 điểm = 3P / 3PA * 100%
  - 2P (2-Point Field Goals Per Game): Số lượng bàn ghi mà là 2 điểm mỗi trận
  - 2PA (2-Point Field Goal Attempts Per Game): Số lân cố gắng ghi bàn 2 điểm mỗi trận
  - 2P% (FG% on 2-Pt FGAs.): Tỉ lệ ghi bàn 2 điểm = 2P / 2PA * 100%
  - eFG% (Effective Field Goal Percentage): Hiệu suất ghi bàn (ghi bàn 3 điểm có trọng số lớn hơn ghi bàn 2 điểm)
  - FT (Free Throws Per Game): Số lần ném phạt mà vào rổ mỗi trận
  - FTA (Free Throw Attempts Per Game): Số lần ném phạt mỗi trận
  - FT% (Free Throw Percentage): Tỉ lệ ném phạt vào rổ
  - ORB (Offensive Rebounds Per Game): Số lần thực hiện offensive rebound mỗi trận [1]
  - DRB (Defensive Rebounds Per Game): Số lần thực hiện defensive rebound mỗi trận [2]
  - TRB (Total Rebounds Per Game): Tổng số lần rebound mỗi trận
  - AST (Assists Per Game): Số lần hỗ trợ ghi bàn mỗi trận
  - STL (Steals Per Game): Số lần cướp bóng mỗi trận
  - BLK (Blocks Per Game): Số lần chặn đối phương ghi bàn mỗi trận
  - TOV (Turnovers Per Game): Số lần mất bóng mỗi trận
  - PF (Personal Fouls Per Game): Số lỗi mỗi trận mắc phải
  - PTS (Points Per Game): Số điểm ghi được mỗi trận

[1] Offensive rebound: khi một người tấn công trong đội A ném trượt, người này cũng trong đội A chụp được quả bóng và thực hiện ném lần hai

[2] Deffensive rebound: khi một người tấn công trong đội A ném trượt, người này trong đội B chặn và chiếm được quả bóng 

### Mức lương
Tiếp theo, ta cần biết mức lương của họ: https://hoopshype.com/salaries/players/


<img src="https://github.com/linanthon/KHDL_DA/blob/master/Image_for_readme/source_salary.png" width=700 height=560>

Trang web sử dụng đơn vị là USD, sau khi lấy về thì nhóm chuyển thành nghìn USD, nhắc lại là chúng tôi chỉ lấy lương của họ trong mùa này nên chỉ lấy cột đầu tiên (2019/20) 

## Thu thập dữ liệu

Theo như tập tin jupyter notebook đính kèm (crawl_data.ipynb) thì sau khi thu thập xong, chúng ta sẽ có được hai dataframe của cầu thủ và mức lương lần lượt như sau:

![alt text](https://github.com/linanthon/KHDL_DA/blob/master/Image_for_readme/data_frame_player.png)

<img src="https://github.com/linanthon/KHDL_DA/blob/master/Image_for_readme/data_frame_salary.png" width=225 height=170>

Ta tiến hành hợp nhất hai bảng này lại với nhau và lưu vào luôn player.csv, trong đó, loại bỏ các cầu thủ không có trong cả hai bảng hoặc cầu thủ có lương không công khai

![alt text](https://github.com/linanthon/KHDL_DA/blob/master/Image_for_readme/player_salary_merged.png)

## Tiền xử lý

Trước tiên, tập train và test được chia theo tỉ lệ 80 – 20.

Với cột Age, giá trị dao động từ 19 đến 42, điều này sẽ khó cho mô hình trong việc đặt trọng số. Dựa vào đồ thị sau, ta chia độ tuổi ra thành 3 nhóm chính:
- Trẻ (Young): <25
- Tuổi vàng (Prime): 25≤ tuổi ≤30
- Lớn tuổi (Old): >30

![alt text](https://github.com/linanthon/KHDL_DA/blob/master/Image_for_readme/barplot_age_salary.png)

Xét cột Pos (vị trí), có một số pos chỉ xuất hiện 1, 2 lần, nếu ta one-hot encode chúng có thể sẽ tạo ra nhiễu. Mà những pos đó là của các tuyển thủ chơi 2 vị trí, nhóm quyết định là những tuyển thủ chơi nhiều vị trí sẽ gộp vô luôn vị trí đầu tiên của họ.

<img src="https://github.com/linanthon/KHDL_DA/blob/master/Image_for_readme/groupby_pos.png" width=284 height=330>

Xem xét độ tương quan giữa các cột, ta thấy có sự liên quan giữa các cột (fg, fga, fgp), (3p, 3pa, 3pp), (2p, 2pa, 2pp), (ft, fta, ftp).
Khi xét độ tương quan của các cột với mức lương thì các cột về tỷ lệ có mức tương quan thấp hơn nhiều so với các cột thường.

<img src="https://github.com/linanthon/KHDL_DA/blob/master/Image_for_readme/corr_all_vs_salary.png" width=340 height=240>

⟹ Các cột tỷ lệ là không cần thiết, bỏ các cột đó đi (fp, 3pp, 2pp, ftp)

Cuối cùng là bỏ đi cột tên. Các cột số nếu có giá trị thiếu sẽ được điền vào bằng mean của cột đó. Còn các cột là category có giá trị thiếu sẽ được điền bằng giá trị phổ biến nhất, sau đó sẽ được one-hot encode.

## Mô hình

Nhóm đã thử với nhiều mô hình regression, nhưng do bản chất dữ liệu có xu hướng tản về hai phía nên khó tìm được "đường" để fit được chúng. Dưới đây là một số kết quả:

<img src="https://github.com/linanthon/KHDL_DA/blob/master/Image_for_readme/results.png" width=425 height=190>

Các mô hình còn dự đoán ra lương âm cho một số tuyển thủ, nếu ra lương âm, thay bằng min lương của tập train.

Nhóm đã thử sử dụng đơn vị khác (triệu USD) và scale cột salary, đều cho ra kết quả không khá hơn.

## Kết luận

Theo bảng số liệu trên, mô hình cho kết quả cao nhất là Elastic Net Regression (cũng chỉ 50% trên tập test).
Kết luận: Độ chính xác còn thấp, không nên trông cậy nhiều, chỉ sử dụng để hỗ trợ.
