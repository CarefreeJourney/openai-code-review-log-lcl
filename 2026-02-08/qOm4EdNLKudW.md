```java
public class OpenAiCodeReview {
    private static final String COMMIT_INFO_FORMAT = "%s_%s_%s";

    public void logCommitDetails(String commitAuthor, String commitMessage) {
        String dateFolder = "logs/" + getCurrentDate();
        File dateFolderFile = new File(dateFolder);
        if (!dateFolderFile.exists()) {
            dateFolderFile.mkdirs();
        }

        String fileName = generateRandomString(12) + ".md";
        // Improved file naming strategy to include commit information for uniqueness
        String finalFileName = String.format(COMMIT_INFO_FORMAT, commitAuthor, commitMessage, generateRandomString(12)) + ".md";
        File logFile = new File(dateFolder, finalFileName);

        try (FileWriter writer = new FileWriter(logFile)) {
            writer.write(log);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    private String generateRandomString(int length) {
        String characters = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789";
        StringBuilder sb = new StringBuilder(length);
        for (int i = 0; i < length; i++) {
            int index = (int) (Math.random() * characters.length());
            sb.append(characters.charAt(index));
        }
        return sb.toString();
    }

    private String getCurrentDate() {
        SimpleDateFormat sdf = new SimpleDateFormat("yyyyMMdd");
        return sdf.format(new Date());
    }
}
```

### 代码评审：

1. **文件命名策略改进**：原来的文件命名方式仅使用随机字符串，这可能导致文件名重复。新策略结合了提交人、提交信息和随机字符串，提高了文件名的唯一性，减少了文件冲突的可能性。

2. **异常处理**：增加了对`FileWriter`的异常处理，确保在文件写入过程中发生异常时能够捕获并打印堆栈跟踪。

3. **日期格式化**：使用`SimpleDateFormat`来格式化日期，确保日志文件按日期存储，便于管理和查询。

4. **代码结构**：代码结构清晰，方法职责明确，易于理解和维护。

5. **可读性**：代码使用了常量来定义文件命名格式，提高了代码的可读性和可维护性。