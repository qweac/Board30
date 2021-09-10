발견 문제점

# 1. WriteDAO.xml

### 원인 : view.do resultType 경로 가 잘못되었음
``` 
//수정
<select id="selectByUid" resultType="com.lec.spring.WriteDTO">
=>
<select id="selectByUid" resultType="com.lec.spring.domain.WriteDTO">
```


# 2. WriteDAO.xml

### 원인 : deleteOk 부분의 SQL 구문 오류

```
//수정
DELETE FROM test_write WHERE uid = #{uid}
=>
DELETE FROM test_write WHERE wr_uid = #{uid}
```

# 3. updateOk.jsp

### 원인 : For input string: ""
```
//수정
location.href = "view.do?uid=${uid}";
=>
location.href = "view.do?uid=${param.uid}";
```

# 4. WriteDAOImpl.java, WriteDAO.java

### 원인 : readByUid 부분이 주석 처리 되어있어 조회수가 증가 하지않음

```
//수정(WriteDAO.java)
//public abstract List<WriteDTO> readByUid(int uid);
=>
public abstract List<WriteDTO> readByUid(int uid);

----------------------------------------------------
//수정(WriteDAOImpl.java)
//	@Override
//	public List<WriteDTO> readByUid(int uid) {
//		mapper.incViewCnt(uid);
//		return mapper.selectByUid(uid);
//	}

=>

@Override
public List<WriteDTO> readByUid(int uid) {
	mapper.incViewCnt(uid);
	return mapper.selectByUid(uid);
}
```
