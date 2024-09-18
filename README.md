# tool

^[0-9][ACDFGHJKLMNPRSTUWXYZ][0-9][ACDFGHJKLMNPRSTUWXYZ]$


^[a-zA-Z0-9 .()]*$
^[1-9][0-9]{0,11}$

StringBuilder
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
import java.time.format.DateTimeFormatter;

        // 获取当前日期时间
        LocalDateTime now = LocalDateTime.now();

        // 创建日期时间格式化器，格式为 yyyy-MM-dd HH:mm
        DateTimeFormatter dateTimeFormatter = DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm");

        // 格式化当前日期时间
        String formattedDateTime = now.format(dateTimeFormatter);

       while (true) {
            try {
                System.out.print("请输入日期和时间（格式 yyyy-MM-dd HH:mm）: ");
                String dateTimeInput = scanner.nextLine();
                LocalDateTime inputDateTime = LocalDateTime.parse(dateTimeInput, dateTimeFormatter);
                break;
            } catch (DateTimeParseException e) {
                // 解析失败
                System.out.println("输入格式错误，请按正确格式输入（例如 2021-12-15 13:45）");
            }
        }
        
    
创建一个方法来检查输入时间是否处于特定的时间范围内

    public static boolean isAccessAllowed(LocalDateTime inputDateTime) {
    // 定义时间限制
    LocalTime startTime = LocalTime.of(8, 0);  // 早上8:00
    LocalTime endTime = LocalTime.of(17, 30);  // 下午5:30

    // 提取输入的时间部分
    LocalTime inputTime = inputDateTime.toLocalTime();

    // 检查当前时间是否在允许的范围内
    return inputTime.isAfter(startTime) && inputTime.isBefore(endTime);

    // 检查当前时间是否在允许的范围内，包括开始和结束时间
    return !inputTime.isBefore(startTime) && !inputTime.isAfter(endTime);
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
    
