# tool
![17a7f2817210aa7c0642318b2d51b074](https://github.com/user-attachments/assets/1404ac6b-ac85-4f2e-bbff-6f2f845de6b1)

给我一个正则表达式 要求 由四位的（半角英文或者半角数字）组成  其中第一位跟第三位只能是数字  其他的可以是英文也可以是数字  其中能使用的英文只有（BEIOQVZ）之外的19个字母 并且英文必须是大写

^[0-9][ACDFGHJKLMNPRSTUWXYZ][0-9][ACDFGHJKLMNPRSTUWXYZ]$

给我一个正则表达式 要求只能是半角英文 半角数字 半角空格 半角. 半角() 组成

^[a-zA-Z0-9 .()]*$
^[1-9][0-9]{0,11}$


对于一个已经得到的对象

StringBuilder stringBuilder = new StringBuilder();
String name4 = pet.getName4() == null ? "" : pet.getName4();
stringBuilder.append(name1 + "," + name2 + "," + name3 + "," + name4 + "\n");


文件写入
 try (PrintWriter writer = new PrintWriter(filePath)) {
            writer.print(stringBuilder.toString());
        } catch (FileNotFoundException e) {}

![image](https://github.com/user-attachments/assets/98630cec-1259-4396-820e-76958e1f5934)

使用HashSet
如果你关心性能，特别是当列表很大时，每次检查都遍历整个列表可能效率不高。你可以使用一个HashSet来存储所有已存在的编号，这样可以以更快的时间复杂度检查重复

    private List<Pet> pets = new ArrayList<>();
    private HashSet<String> ids = new HashSet<>();

    public boolean addPet(Pet newPet) {
        if (ids.contains(newPet.getId())) {
            return false;  // 发现编号重复，不添加
        }
        pets.add(newPet);  // 未发现重复，添加到列表
        ids.add(newPet.getId());  // 添加编号到HashSet中
        return true;
    }


如何读取文件时就把ID放HashSet 
            while ((line = reader.readLine()) != null) {
                String[] parts = line.split(","); // 按逗号分隔每一行
                if (parts.length > 0) {
                    ids.add(parts[0].trim()); // 提取第一个元素并添加到HashSet中，trim()用于去除可能的空格
                }
            }

![image](https://github.com/user-attachments/assets/b4e39dc6-c138-4c49-86af-226b05fe441d)

如何使用LocalDateTime

import java.time.LocalDateTime;
// 获取当前的日期和时间
LocalDateTime now = LocalDateTime.now();
// 从LocalDateTime对象中获取分钟
int minute = now.getMinute();


创建一个方法来检查当前时间是否处于特定的时间范围内
    public static boolean isAccessAllowed() {
        // 定义时间限制
        LocalTime startTime = LocalTime.of(8, 0);  // 早上8:00
        LocalTime endTime = LocalTime.of(17, 30);  // 下午5:30

        // 获取当前时间
        LocalTime now = LocalTime.now();

        // 检查当前时间是否在允许的范围内
        return now.isAfter(startTime) && now.isBefore(endTime);
    }
    
检查输入的日期时间是否为过去的时间
        public static boolean isValidDateTime(LocalDateTime dateTime) {
        // 获取当前日期时间
        LocalDateTime now = LocalDateTime.now();

        // 检查输入的日期时间是否在当前日期时间之前
        return dateTime.isBefore(now);
    }
    
![image](https://github.com/user-attachments/assets/87c1e132-5fd7-4039-9f94-a466ceeb933c)
四舍五入

import java.math.BigDecimal;
import java.math.RoundingMode;
        BigDecimal value = new BigDecimal("123.4567");
        // 保留两位小数，使用四舍五入模式
        BigDecimal roundedValue = value.setScale(2, RoundingMode.HALF_UP);

 ![image](https://github.com/user-attachments/assets/21a67556-8bd7-4552-890f-178250d8c9bb)

import java.util.Collections;  // 导入 Collections 类
import java.util.List;
import java.util.ArrayList;  
import java.util.Comparator; 
       
    public static void sortPetsByAgeDesc(List<Pet> pets) {
        pets.sort((p1, p2) -> Integer.compare(p2.getAge(), p1.getAge()));//这个是新版本 
        Collections.sort(pets, (p1, p2) -> Integer.compare(p2.getAge(), p1.getAge()));//这个是老版本  对于 Collections.sort()，除了需要 List 和 Comparator，还必须导入 Collections 类

    }
        
        sortPetsByAgeDesc(pets);

        System.out.println("After sorting:");
        pets.forEach(System.out::println);
    
