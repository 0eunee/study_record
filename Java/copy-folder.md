# 폴더와 폴더 안의 파일 복사하기
```java
public void makeCopyFile() throws Exception {
	// 경로 (Config.properties)
	Properties prop = new Properties();
	ClassLoader cl;
	cl = Thread.currentThread().getContextClassLoader();
	URL configUrl = cl.getResource("Config.properties");
	prop.load(configUrl.openStream());
	String uploadPath = prop.getProperty("fileUploadPath");

	File sourceF = new File("/file");
	File targetF = new File(uploadPath);

	copyFile(sourceF, targetF);
}

public void copyFile(File sourceF, File targetF) throws Exception {
	File[] target_file = sourceF.listFiles();

	for (File file : target_file) {
		File temp = new File(targetF.getAbsolutePath() + File.separator + file.getName());

		if (file.isDirectory()) {
			temp.mkdir();
			copyFile(file, temp);
		} else {
			FileInputStream fis = null;
			FileOutputStream fos = null;
			try {
				fis = new FileInputStream(file);
				fos = new FileOutputStream(temp);
				byte[] b = new byte[4096];
				int cnt = 0;
				while((cnt=fis.read(b)) != -1) {
					fos.write(b, 0, cnt);
				}
			} catch (Exception e) {
				e.printStackTrace();
			} finally {
				try {
					fis.close();
					fos.close();
				} catch (IOException e) {
					e.printStackTrace();
				}
			}
		}
	}
}
```
- 출처 : [자바로 폴더(디렉토리),파일 복사하기](https://coding-factory.tistory.com/285)
