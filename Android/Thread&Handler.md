### 20211228  

### 스레드란?  
프로그램에서 실행되는 흐름의 단위이다.  

### 언제 사용 할까?  
앱을 구현할 때 두개의 기능이 동시에 실행되어야 할 때가 있다.  
현재 실행되고 있는 코드와 별도로 시스템에서 자원을 할당하여, 동시에 실행시켜 준다.  

### 서비스 vs 스레드  
서비스는 UI없이 동작하고, 스레드는 UI에 접근하여 수정하는 것이 가능하다.  

### Handler란?  
여러가지 스레드가 동시에 UI에 접근함으로써 Deadlock과 같은 Concurrency Problem이 발생할 수 있다.  
이때 안드로이드에서는 Handler를 통해 UI에 접근하도록 하고 있다.  
Message Queue를 이용하여 Main Thread에서 순차적으로 코드를 수행할 수 있게 해준다.  

### Runnable이란?  
Run 메소드를 가지는 간단한 인터페이스로써, 스레드 대신에 run 메소드를 제공하는 역할을 한다.  

### 총평  
즉, 기존에 존재하는 하나의 메인 스레드에 별도의 스레드를 생성하여 자원을 할당하면 동시에 실행이 가능하다.  
이때 스레드는 서비스와 달리 UI에 접근하여 작업할 수 있다. 하지만 동시에 UI를 작업하다 보면 문제가 생길 수 있고  
이를 방지하기 위해서 Handler에 run 객체 또는 인자를 넘겨주어서 사용하면 Message Queue에 보관하여 Main Thread에서 순차적으로 실행할 수 있다.
