## 返回客户端Json模型
```java
/**
 * <p>响应json数据</p>
 * @author imant@outlook.com
 * @date 2016-9-9 下午3:41:29
 */
public class ResponseVo {
	private String code = "200";
	private String message;
	private Object obj;
	
	public ResponseVo() {
	}
	
	public ResponseVo(String code, String message) {
		this.code = code;
		this.message = message;
	}
	
	public void success(String message) {
		this.message = message;
	}
	
	public void success(String message, Object obj) {
		this.message = message;
		this.obj = obj;
	}
	
	public void fatal(String message) {
		this.code = "500";
		this.message = message;
	}
	
	public void fatal(String message, Object obj) {
		this.code = "500";
		this.message = message;
		this.obj = obj;
	}
	
	public String getCode() {
		return code;
	}

	public void setCode(String code) {
		this.code = code;
	}

	public String getMessage() {
		return message;
	}

	public void setMessage(String message) {
		this.message = message;
	}

	public Object getObj() {
		return obj;
	}

	public void setObj(Object obj) {
		this.obj = obj;
	}

}

```