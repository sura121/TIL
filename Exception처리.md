## Restful Exception

**@ExceptionHandler 방식**
```
@ExceptionHandler에 여러개의 Exception을 설정할 수 있으며 해당 Controller에서 Exception이 발상하면  handleException이 처리를 담당한다.
단점은 해당 Controller에서만 처리를 한다는 것이다.
```
**@ControllerAdvice 방식**
```
@ControllerAdvice 방식은 전역(글로벌)하게 예외처리가 가능하다.
@ExceptionHandler를 이용하여 어떤 Exception을 처리 할 것인지 결정해주면된다.
```
***
## @ExceptionHandler

**Controller 안에**
```
@ExceptionHandler(TitleNotException.class)
public ErrorDetail myError(HttpServletRequest
request, Exception ex){
 ErrorDetail error = new ErrorDetail();
 error.setStatus(HttpStatus.BAD_REQUEST.value());
 error.setMessage(ex.getLocalizedMessage());
 error.setURL().append("/error").toString();
 return error;
}
```

**TitleNotException.java**
```

public class TitleNotException extends RuntimeException {

	/**
	 * 
	 */
	private static final long serialVersionUID = 1L;
	public TitleNotException (String title){
		super("제목을 입력하십시오.");
	}

}
```

**DetailError**
```
public class ErrorDetail {
	
	private int status;
	private String message;
	private String url;
	public int getStatus() {
		return status;
	}
	public void setStatus(int status) {
		this.status = status;
	}
	public String getMessage() {
		return message;
	}
	public void setMessage(String message) {
		this.message = message;
	}
	public String getUrl() {
		return url;
	}
	public void setUrl(String url) {
		this.url = url;
	}
	
	

}
```
