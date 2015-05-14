# Wannianli
实现了日历的查询，方便使用。界面主要是由查询输入部分和结果显示部分两部分组成。


实验完整源码

package yly; 
import java.applet.Applet; 
import javax.swing.*; 
import java.awt.*;  
import java.awt.event.ActionEvent; 
import java.awt.event.ActionListener; 
import java.util.Calendar; 
import java.util.Date; 
  public class rili extends JFrame implements ActionListener { 
  JButton b_today, b_query;  
JLabel lb_Year, lb_Month;
  JButton b_week[] = new JButton[7];  
JButton b_day[][] = new JButton[6][7];  
Container thisContainer; 
 JPanel pUp;  
JPanel pCenter;  
JPanel pCenter_week, pCenter_day;  
JComboBox year, month;  
public void init() {  
b_today = new JButton("今天"); 
b_query = new JButton("查询");  
setTitle("日历");
lb_Year = new JLabel("Year");  
lb_Month = new JLabel("Month"); 
year = new JComboBox(); 
month = new JComboBox(); 
setDate();  
pUp = new JPanel();  
pUp.add(lb_Year); 
pUp.add(year);  
pUp.add(lb_Month);  
pUp.add(month);  
pUp.add(b_today);  
pUp.add(b_query); 
b_today.addActionListener(this);  
b_query.addActionListener(this);  
pCenter = new JPanel();  
pCenter_week = new JPanel();  
b_week[0] = new JButton("星期日");  
b_week[1] = new JButton("星期一");  
b_week[2] = new JButton("星期二");  
b_week[3] = new JButton("星期三");  
b_week[4] = new JButton("星期四");  
b_week[5] = new JButton("星期五");  
b_week[6] = new JButton("星期六"); 
b_week[0].setSize(400, 200); 
b_week[1].setSize(400, 200);  
b_week[2].setSize(400, 200);  
b_week[3].setSize(400, 200);  
b_week[4].setSize(400, 200);  
b_week[5].setSize(400, 200); 
b_week[6].setSize(400, 200);  
for (int i = 0; i < 7; i++){  
b_week[i].setEnabled(false); 
 pCenter_week.add(b_week[i]); 
}  
 pCenter_day = new JPanel();  
 for (int cols = 0; cols < 6; cols++) { 
 for (int rows = 0; rows < 7; rows++) { 
 b_day[cols][rows] = new JButton(""); 
 b_day[cols][rows].setSize(400, 200);  
this.pCenter_day.add(b_day[cols][rows]); 
        } 
 }  
 pCenter_day.setLayout(new GridLayout(6, 7));  
 setDay(Integer.parseInt(this.year.getSelectedItem().toString()), 
 Integer.parseInt(this.month.getSelectedItem().toString())); 
 // setDay(2011,2);  
 pCenter.setLayout(new BorderLayout()); 
 pCenter.add(pCenter_week, "North"); 
 pCenter.add(pCenter_day, "Center"); 
 thisContainer = this.getContentPane();  
 thisContainer.setLayout(new BorderLayout()); 
 thisContainer.add(pUp, "North"); 
 thisContainer.add(pCenter, "Center"); 
 this.setVisible(true); 
 this.setResizable(false);  
this.pack();  
      }  
 public void setDate() {  
int year, month, day, week; 
 Calendar cal = Calendar.getInstance(); 
 year = cal.get(Calendar.YEAR); 
  month = cal.get(Calendar.MONTH);  
  day = cal.get(Calendar.DATE);  
 week = cal.get(Calendar.WEEK_OF_YEAR); 
  int year_temp = year - 4; 
  for (int i = 0; i < 10; i++) { 
  this.year.addItem(year_temp); 
  year_temp += 1; 
 }  
 this.year.setSelectedIndex(4); 
 for (int n = 0; n < 12; n++) { 
 this.month.addItem(n + 1); 
} 
this.month.setSelectedIndex(month);  
}  
 public void setDay(int Year, int Month) { 
 int count; 
Calendar c = Calendar.getInstance();  
 c.clear();  
c.set(Year, Month-1, 1);  
count = c.getActualMaximum(Calendar.DAY_OF_MONTH); 
//总天数
 System.out.print(count); 
 int day = c.get(Calendar.DAY_OF_WEEK) - 1; 
// 0为星期天，6为星期六 
System.out.print(day); 
 int i = 1 - day;  
for (int cols = 0; cols < 6; cols++) {  
for (int rows = 0; rows < 7; rows++) {  
String st = String.valueOf(i);  
b_day[cols][rows].setText(st);  
b_day[cols][rows].setEnabled(false); 
 if (i > 0 && i <= count) 
 b_day[cols][rows].setVisible(true);  
else  
b_day[cols][rows].setVisible(false);  
i++; 
           } 
}  
}   
public void actionPerformed(ActionEvent e) { 
if (e.getSource() == b_query) {   
this.setDay(Integer.parseInt(this.year.getSelectedItem().toString()), Integer.parseInt(this.month.getSelectedItem().toString()));   
}   
if (e.getSource() == b_today) {  
int year, month;  
Calendar cal = Calendar.getInstance();  
year = cal.get(Calendar.YEAR);  
month = cal.get(Calendar.MONTH)+1;  
this.setDay(year,month); 
  } 
}   
public static void main(String[] args) {  
rili rl = new rili();  
rl.init(); 
}  
}  
