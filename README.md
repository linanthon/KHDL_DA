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
  - STL (Steals Per Game): Số lần cướp bàn ghi mỗi trận
  - BLK (Blocks Per Game): Số lần chặn đối phương ghi bàn mỗi trận
  - TOV (Turnovers Per Game): Số lần phản bóng mỗi trận
  - PF (Personal Fouls Per Game): Số lỗi mỗi trận mắc phải
  - PTS (Points Per Game): Số điểm ghi được mỗi trận

[1] Offensive rebound: khi một người tấn công trong đội A ném trượt, người này cũng trong đội A chụp được quả bóng và thực hiện ném lần hai

[2] Deffensive rebound: khi một người tấn công trong đội A ném trượt, người này trong đội B chặn và chiếm được quả bóng 

### Mức lương
Tiếp theo, ta cần biết mức lương của họ: https://hoopshype.com/salaries/players/

![alt text](https://github.com/linanthon/KHDL_DA/blob/master/Image_for_readme/source_salary.png)

Trang web này thì không có gì nhiều cần chú thích, nhắc lại là chúng tôi chỉ lấy lương của họ trong mùa này nên chỉ lấy cột đầu tiên (2019/20) 

## Thu thập dữ liệu

Theo như tập tin jupyter notebook đính kèm (crawl_data.ipynb) thì sau khi thu thập xong, chúng ta sẽ có được hai dataframe của cầu thủ và mức lương lần lượt như sau:

![alt text](https://github.com/linanthon/KHDL_DA/blob/master/Image_for_readme/data_frame_player.png)

![alt text](https://github.com/linanthon/KHDL_DA/blob/master/Image_for_readme/data_frame_salary.png)

Ta tiến hành hợp nhất hai bảng này lại với nhau và lưu vào luôn player.csv:

![alt text](https://github.com/linanthon/KHDL_DA/blob/master/Image_for_readme/player_salary_merged.png)

## Tiền xử lý

...

## Huấn luyện mô hình và kiểm thử

...
