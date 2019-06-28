# 17 Spring Bean ����ע��
��������ʹ�������׼�� Spring ��ܼ������������� bean �͹�������ע�롣Ϊ�˼򵥣����Ǿ�������ʹ�� @ComponentScan ��������� bean����ʹ�� @Autowired ��������ע�룩Ч���ܺã�work well����
<!-- more -->
�����������Ľ��鹹����Ĵ��루�ڸ����ж�λӦ�ó����ࣩ������������ɵģ�without arguments����� @ComponentScan����Ӧ�õ����������@Component��@Service��@Repository��@Controller�������Զ�ע�ᵽ Spring bean�

����ʵ��չʾ��һ�� @Service bean����ʹ�ÿ�����ע���Ի�ñ�Ҫ�� `RiskAssessor` bean��

```java
package com.example.service;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

@Service
public class DatabaseAccountService implements AccountService {

	private final RiskAssessor riskAssessor;

	@Autowired
	public DatabaseAccountService(RiskAssessor riskAssessor) {
		this.riskAssessor = riskAssessor;
	}

	// ...

}
```
