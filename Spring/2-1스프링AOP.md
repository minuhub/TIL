## 스프링 AOP
클래스-serviceImpl-스프링설정파일(.xml)-Client구조에서

serviceImpl에 구현되어진 메소드들(어떤 기능에 해당)을 Jointpoint(비즈니스 메소드)이라고 함
비즈니스 메소드들중 몇가지가 공통으로 가지는 기능을 advice(어드바이스 메소드) 라고함
jointpoint중 advice라는 공통기능을 가질 애들을 필터링해서 Pointcut이라고 함
Pointcut을 필터링해서, advice를 주는 과정을 Aspect설정이라고 함

이때 2가지를 고려해야함
advice의 동작 시점을 언제로 지정해줄지
advice에 pointcut의 정보와 바인드변수를 매개변수로 주기

## AOP설정 과정
일반적인 경우
어드바이스 클래스 구현후 1 or 2
1. 스프링 설정 파일에서 <aop:aspect>로 aspect설정
2. annotation설정

트랜잭션의 경우
어드바이스 클래스 구현 X
스프링 설정 파일에 트랜잭션 관리자 등록
스프링 설정 파일에  어드바이스 설정을 위해 <tx:advice>등록(이때 <tx:advice>내부에서 트랜잭션 관리자 지정)
스프링 컨테이너가 <tx:advice>를 참조하여  트랜잭션 관리 기능 어드바이스 생성
스프링 설정 파일에서 <aop:advisor>로 aspect설정

## 구조 예시
.xml에서
```xml
<bean id="log" class="com.springbook.biz.common.logAdvice"></bean>
//advice객체

<aop:config>
	<aop:pointcut id="getPointcut" expression="execution(* com.springbook.biz..*Impl.get*(..)"/>
	//포인트컷설정
	<aop:aspect ref="log">
		<aop:before pointcut-ref="getPointcut" method="printLog"/>
		//aop객체의 메소드를 pointcut과 연결해주는 aspect설정
	</aop:aspect>
</aop:config>
```
