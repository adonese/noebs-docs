### noebs Java SDK


Add jitpack to your build.gradle

```sh
repositories {
        ...
        maven { url 'https://jitpack.io' }
    }
```

Add the sdk to your dependancies
  
```sh
	dependencies {
	        implementation 'com.github.fakhrisati:solussdk:1.0.0'
	}
 ```

```java
public static void main(String[] args) {
		Payment payment = new Payment("gdljdfslkgjf;lgks", "31323232323", "3232", "3232", 1f, "0010050307");
		NOEBSClient noebsClient = new NOEBSClient();
		BaseResponse<?> response = noebsClient.getResponse(payment);
		Object object = response.getResponse();
		if(object instanceof Response) {
			System.out.println(true);
			// handle response cases here
		}else if(object instanceof ErrorResponse){
			ErrorResponse err =(ErrorResponse)object;
			System.out.println(err.getMessage());
			 Map<String, String> details = err.getDetails();
			if(!details.isEmpty())///if details not empty show messages
				 for(Map.Entry m:details.entrySet()){  
					   System.out.println(m.getKey()+" : "+m.getValue());  
					  }
			System.out.println(false);
		}else {
			System.out.println("Error");
		}
		
	}
```