# 自定义注解

可以用于公共字段的填充

## 常量类,枚举类
```java
public class AutoFillConstant {
    /**
     * 实体类中的方法名称
     */
    public static final String SET_CREATE_TIME = "setCreateTime";
    public static final String SET_CHANGE_TIME = "setChangeTime";
}
public enum OperationType {
    //更新以及插入操作
    UPDATE,
    INSERT
}
```

## 定义切面

```java
/**
 * 自定义切面,实现公共字段填充处理逻辑
 */
@Aspect
@Component
@Slf4j
public class AutoFillAspect {
    /**
     * 切入点
     */
    @Pointcut("execution(* com.ling.mappers.*.*(..)) && @annotation(com.ling.annotation.AutoFill)")
    public void autoFillPointCut() {
    }

    /**
     * 前置通知,在通知中会为公共字段赋值
     */
    @Before("autoFillPointCut()")
    public void autoFill(JoinPoint joinPoint) {
        log.info("开始进行公共字段填充...");
        //获取被拦截方法上的数据库操作类型
        MethodSignature signature = (MethodSignature) joinPoint.getSignature();//方法签名对象
        AutoFill annotation = signature.getMethod().getAnnotation(AutoFill.class);//获取方法上的注解对象
        OperationType operationType = annotation.value();//获得数据库的操作类型
        //获取当前被拦截的方法的参数--实体对象
        Object[] args = joinPoint.getArgs();
        if (args == null || args.length == 0) {
            return;
        }
        Object entity = args[0];
        //准备赋值的数据
        LocalDateTime now = LocalDateTime.now();
        //根据当前不同的操作类型,为应属性进行反射赋值
        if (operationType == OperationType.INSERT || operationType == OperationType.UPDATE) {
            //为插入操作的四个公共字段赋值
            try {
                Method setCreateTime = entity.getClass().getDeclaredMethod(AutoFillConstant.SET_CREATE_TIME, LocalDateTime.class);
                Method setChangeTime = entity.getClass().getDeclaredMethod(AutoFillConstant.SET_CHANGE_TIME, LocalDateTime.class);

                //通过反射为对象赋值
                setCreateTime.invoke(entity, now);
                setChangeTime.invoke(entity, now);

            } catch (Exception e) {
                e.printStackTrace();
            }


        } else {
            System.out.println("OperationType 有误!");
        }
    }
}
```