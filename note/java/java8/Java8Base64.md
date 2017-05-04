# Java8 base64 res note #

## base64作用 ##

java8 base64只是起到转码的作用，将数据编码成不易识别的字符串

## 常见应用领域 ##
1. 图片编码，存放到数据库中text字段里面

## 代码示例 ##
1. 编码/解码案例

    public class Java8Base64Test {

	@Test
	public void arrayTest() {
		try {

			// Encode using basic encoder
			String base64encodedString = Base64.getEncoder().encodeToString("java8%".getBytes("utf-8"));
			System.out.println("Base64 Encoded String (Basic) :" + base64encodedString);

			// Decode !SRQOlRdOgTkOfYYOfIKOgIhOgOIOffg
			byte[] base64decodedBytes = Base64.getDecoder().decode(base64encodedString);

			System.out.println("Original String: " + new String(base64decodedBytes, "utf-8"));
			base64encodedString = Base64.getUrlEncoder().encodeToString("java8%".getBytes("utf-8"));
			System.out.println("Base64 Encoded String (URL) :" + base64encodedString);
			
			base64encodedString = Base64.getMimeEncoder().encodeToString("java8%".getBytes());
			System.out.println("Base64 Mime Encode :"  + base64encodedString);

			StringBuilder stringBuilder = new StringBuilder();

			for (int i = 0; i < 10; ++i) {
				stringBuilder.append(UUID.randomUUID().toString());
			}

			byte[] mimeBytes = stringBuilder.toString().getBytes("utf-8");
			String mimeEncodedString = Base64.getMimeEncoder().encodeToString(mimeBytes);
			System.out.println("Base64 Encoded String (MIME) :" + mimeEncodedString);
			
			System.out.println(new String(Base64.getMimeDecoder().decode(mimeEncodedString),"utf-8"));
		} catch (UnsupportedEncodingException e) {
			System.out.println("Error :" + e.getMessage());
		}
	}}
