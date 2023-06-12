---
layout: single
title:  "[Java] 1차 프로젝트(회원가입)"
# categories: Java-1차Project
Projects: Java-1차Project
toc: true
---

<br/><br/>
siksin이라는 맛집검색 홈페이지를 벤치마킹

MVC모델로 개발을 하였음. 

데이터베이스와 자바의 연동
<br/><br/>


# action - Action #

```java
package min.java.Siksin.action;

import java.util.Scanner;

public interface SiksinMemberAction {

	public void execute(Scanner scanner);
	
}

```
<br/>


# service - Service #

```java
package min.java.Siksin.service;

import java.util.ArrayList;
import min.java.Siksin.DTO.SiksinMemberDTO;

public interface SiksinMemberService {

	public ArrayList<SiksinMemberDTO> SiksinMemberSelectAll();

	public void SiksinMemberInsert(SiksinMemberDTO siksinMemberDTO);

	public SiksinMemberDTO SiksinMemberUpdate(String memberEmail, String password, String nickName, String phoneNum, String memberArea);

	public SiksinMemberDTO SiksinMemberDelete(String memberEmail);

	public SiksinMemberDTO SiksinMemberSelectD(String memberEmail);

	public SiksinMemberDTO memberEmailcheck(String memberEmail);

}

```
<br/>


# DTO #

```java
package min.java.Siksin.DTO;

public class SiksinMemberDTO {
	private int memberNum;
	private String memberEmail;
	private String password;
	private String nickName;
	private String memberBirth;
	private String gender;
	private String phoneNum;
	private String memberArea;
	
	public int getMemberNum() {
//		System.out.println("DTO- getMemberNum");
		return memberNum;
	}
	public void setMemberNum(int memberNum) {
//		System.out.println("DTO- setMemberNum");
		this.memberNum = memberNum;
	}
	public String getMemberEmail() {
//		System.out.println("DTO- getEmail");
		return memberEmail;
	}
	public void setMemberEmail(String memberEmail) {
//		System.out.println("DTO- setEmail");
		this.memberEmail = memberEmail;
	}
	public String getPassword() {
//		System.out.println("DTO- getPassword");
		return password;
	}
	public void setPassword(String password) {
//		System.out.println("DTO- setPassword");
		this.password = password;
	}
	public String getNickName() {
//		System.out.println("DTO에서 값 확인get"+nickName);
		return nickName;
	}
	public void setNickName(String nickName) {
//		System.out.println("DTO에서 값 확인set"+nickName);
		this.nickName = nickName;
	}
	public String getMemberBirth() {
		return memberBirth;
	}
	public void setMemberBirth(String memberBirth) {
		this.memberBirth = memberBirth;
	}
	public String getGender() {
		return gender;
	}
	public void setGender(String gender) {
		this.gender = gender;
	}
	public String getPhoneNum() {
		return phoneNum;
	}
	public void setPhoneNum(String phoneNum) {
		this.phoneNum = phoneNum;
	}
	public String getMemberArea() {
		return memberArea;
	}
	public void setMemberArea(String memberArea) {
		this.memberArea = memberArea;
	}
	
	@Override
	public String toString() {
		return "SiksinMemberDTO [memberNum=" + memberNum + ", memberEmail=" + memberEmail + ", password=" + password
				+ ", nickName=" + nickName + ", memberBirth=" + memberBirth + ", gender=" + gender + ", phoneNum="
				+ phoneNum + ", memberArea=" + memberArea + "]";
	}
	
}

```
<br/>


# DAO #

```java
package min.java.Siksin.DAO;

import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.util.ArrayList;
import javax.sql.DataSource;
import org.apache.commons.logging.Log;
import org.apache.commons.logging.LogFactory;
import min.java.Siksin.DTO.SiksinMemberDTO;
import min.java.Siksin.dbcp.SiksinContext;
import min.java.Siksin.service.SiksinMemberService;

public class SiksinMemberDAO implements SiksinMemberService {

	private static final Log log = LogFactory.getLog(SiksinMemberDAO.class);

	@Override
	public ArrayList<SiksinMemberDTO> SiksinMemberSelectAll() {

		Connection connection = null;
		PreparedStatement preparedStatement = null;
		ResultSet resultSet = null;
		ArrayList<SiksinMemberDTO> arrayList = new ArrayList<SiksinMemberDTO>();

		try {
			SiksinContext siksinContext = new SiksinContext();
			DataSource dataSource = siksinContext.basicDataSource;
			connection = dataSource.getConnection();

			String sql = "select memberNum, memberEmail, password, nickName, to_char(memberBirth, 'yyyy-mm-dd')memberBirth , gender, phoneNum, memberArea from siksinMember ";
			/* to_char(memberBirth, 'yyyy-mm-dd')memberBirth(뒤에잇는 맴버벌스는 별칭을 의미함) */
			
			log.info("DAO_SelectAll_SQL - " + sql);

			preparedStatement = connection.prepareStatement(sql);
			resultSet = preparedStatement.executeQuery(); // PreparedStatement 개체에서 SQL 쿼리를 실행하고 쿼리에 의해 생성된 ResultSet 개체를 반환합니다.

			// 커서를 현재 위치에서 한 행 앞으로 이동하면서 반복한다.
			while (resultSet.next()) {
				SiksinMemberDTO siksinMemberDTO = new SiksinMemberDTO();
				siksinMemberDTO.setMemberNum(resultSet.getInt("memberNum"));
				siksinMemberDTO.setMemberEmail(resultSet.getString("memberEmail"));
				log.info("DAO_SelectAll회원 이메일 확인" + resultSet.getString("memberEmail"));
				siksinMemberDTO.setPassword(resultSet.getString("password"));
				siksinMemberDTO.setNickName(resultSet.getString("nickName"));
				siksinMemberDTO.setMemberBirth(resultSet.getString("memberBirth"));
				siksinMemberDTO.setGender(resultSet.getString("gender"));
				siksinMemberDTO.setPhoneNum(resultSet.getString("phoneNum"));
				siksinMemberDTO.setMemberArea(resultSet.getString("memberArea"));

				arrayList.add(siksinMemberDTO);// 내가 디티오에서 호출해서 값을 저장한걸 어레이리스트에 저장한다.
				log.info("DAO_SelectAll 조회 데이터 확인 - " + siksinMemberDTO);
			}
			resultSet.getRow();
			if (resultSet.getRow() == 0) {
				log.info("DAO_SelectAll등록한 회원이 없습니다.");
			}

		} catch (Exception e) {
			log.info("DAO_SelectAll전체조회 실패 (예외확인) - " + e);

		} finally {
			try {
				resultSet.close();
				preparedStatement.close();
				connection.close();
				
			} catch (SQLException e) {
				e.printStackTrace();
			}
		}
		return arrayList;

	}

	@Override
	public void SiksinMemberInsert(SiksinMemberDTO siksinMemberDTO) {

		Connection connection = null;
		PreparedStatement preparedStatement = null;

//		내가 DTO로 바로 매개변수로 받았기 때문에 DTO로 저장하는 이코드는 필요가 없어
//		SiksinMemberDTO siksinMemberDTO = new SiksinMemberDTO();
//		siksinMemberDTO.setMemberNum(memberNum);
//		siksinMemberDTO.setMemberEmail(memberEmail);
//		siksinMemberDTO.setPassword(password);
//		siksinMemberDTO.setNickName(nickName);
//		siksinMemberDTO.setMemberBirth(memberBirth);
//		siksinMemberDTO.setGender(gender);
//		siksinMemberDTO.setPhoneNum(phoneNum);
//		siksinMemberDTO.setMemberArea(memberArea);

		try {
//			System.out.println("DAO-inser");

			// 내가 만든 연결 클래스를 인스턴스화해야함
			SiksinContext siksinContext = new SiksinContext();
			DataSource dataSource = siksinContext.basicDataSource;
			connection = dataSource.getConnection();

			String sql = "insert into siksinMember(memberNum, memberEmail, password, nickName, memberBirth, gender, phoneNum, memberArea) ";
			sql += " values(board_seq.nextval, ?, ?, ?, ?, ?, ?, ?) ";
			log.info("DAO_inser_SQL - " + sql);
			preparedStatement = connection.prepareStatement(sql);

			preparedStatement.setString(1, siksinMemberDTO.getMemberEmail());
			preparedStatement.setString(2, siksinMemberDTO.getPassword());
			preparedStatement.setString(3, siksinMemberDTO.getNickName());
			preparedStatement.setString(4, siksinMemberDTO.getMemberBirth());
			preparedStatement.setString(5, siksinMemberDTO.getGender());
			preparedStatement.setString(6, siksinMemberDTO.getPhoneNum());
			preparedStatement.setString(7, siksinMemberDTO.getMemberArea());

			int count = preparedStatement.executeUpdate();
			log.info("DAO_inser_입력 데이터 확인 - " + siksinMemberDTO);
			
			if (count > 0) {
				connection.commit();
				log.info("DAO_inser_커밋되었습니다.");
			} else {
				connection.rollback();
				log.info("DAO_inser_롤백되었습니다.");
			}
		} catch (SQLException e) {
			log.info("DAO_inser_회원 입력 실패 - " + e);
		} finally {
			try {
				preparedStatement.close();
				connection.close();
			} catch (SQLException e) {
				e.printStackTrace();
			}
		}
	}

	@Override
	public SiksinMemberDTO SiksinMemberUpdate(String memberEmail, String password, String nickName, String phoneNum,
			String memberArea) {

		Connection connection = null;
		PreparedStatement preparedStatement = null;

		// 여기는 매개변수를 각각 받았기 때문에 이걸 써줘야해
		SiksinMemberDTO siksinMemberDTO = new SiksinMemberDTO();
		siksinMemberDTO.setMemberEmail(memberEmail);
		siksinMemberDTO.setPassword(password);
		siksinMemberDTO.setNickName(nickName);
		siksinMemberDTO.setPhoneNum(phoneNum);
		siksinMemberDTO.setMemberArea(memberArea);
		try {
			SiksinContext siksinContext = new SiksinContext(); // 내가 만든 연결 클래스를 인스턴스화해야함
			DataSource dataSource = siksinContext.basicDataSource;
			connection = dataSource.getConnection();
			String sql = "update siksinMember set password = ? , nickName = ?,  phoneNum = ? , memberArea = ?  where  memberEmail = ?";

			log.info("DAO_Update_SQL - " + sql);
			preparedStatement = connection.prepareStatement(sql);

			preparedStatement.setString(1, siksinMemberDTO.getPassword());
			preparedStatement.setString(2, siksinMemberDTO.getNickName());
			preparedStatement.setString(3, siksinMemberDTO.getPhoneNum());
			preparedStatement.setString(4, siksinMemberDTO.getMemberArea());
			preparedStatement.setString(5, siksinMemberDTO.getMemberEmail());
			int count = preparedStatement.executeUpdate();

			log.info("DAO_Update_수정데이터 확인 - " + siksinMemberDTO);
			if (count > 0) {
				connection.commit();
				log.info("DAO_Update_커밋되었습니다.");
			} else {
				connection.rollback();
				log.info("DAO_Update_롤백되었습니다.");

			}
		} catch (Exception e) {
			log.info("DAO_Update_회원수정 실패 - " + e);
		} finally {
			try {
				preparedStatement.close();
				connection.close();
			} catch (Exception e) {
				e.printStackTrace();
			}
		}
		return siksinMemberDTO;
	}

	@Override
	public SiksinMemberDTO SiksinMemberDelete(String memberEmail) {

		Connection connection = null;
		PreparedStatement preparedStatement = null;
		SiksinMemberDTO siksinMemberDTO = new SiksinMemberDTO();
		siksinMemberDTO.setMemberEmail(memberEmail);

		try {
			SiksinContext siksinContext = new SiksinContext(); // 내가 만든 연결 클래스를 인스턴스화해야함
			DataSource dataSource = siksinContext.basicDataSource;
			connection = dataSource.getConnection();
			String sql = "delete from siksinMember where memberEmail = ? ";

			log.info("DAO_Delete_SQL - " + sql);
			preparedStatement = connection.prepareStatement(sql);
			preparedStatement.setString(1, siksinMemberDTO.getMemberEmail());

			int count = preparedStatement.executeUpdate();// insert, update, delete 에서 preparedStatement 객체에서 sql문을 싱행합니다.

			if (count > 0) {
				connection.commit();
				log.info("DAO_Delete_커밋되었습니다.");
			} else {
				connection.rollback();
				log.info("DAO_Delete_롤백되었습니다.");
			}
		} catch (SQLException e) {
			log.info("DAO_Delete_회원 삭제 실패 - " + e);
		} finally {
			try {
				preparedStatement.close();
				connection.close();
			} catch (SQLException e) {
				e.printStackTrace();
			}
		}
		return siksinMemberDTO;
	}

	@Override
	public SiksinMemberDTO SiksinMemberSelectD(String memberEmail) {

		Connection connection = null;
		PreparedStatement preparedStatement = null;
		ResultSet resultSet = null;
		SiksinMemberDTO siksinMemberDTO = new SiksinMemberDTO();

		try {
			SiksinContext siksinContext = new SiksinContext(); // 내가 만든 연결 클래스를 인스턴스화해야함
			DataSource dataSource = siksinContext.basicDataSource;
			connection = dataSource.getConnection();

			String sql = "select memberNum, memberEmail, password, nickName, to_char(memberBirth, 'yyyy-mm-dd')memberBirth, gender, phoneNum, memberArea from siksinMember ";
			sql += " where memberEmail = ? ";

			log.info("DAO_SelectD_SQL - " + sql);

			preparedStatement = connection.prepareStatement(sql);
			preparedStatement.setString(1, memberEmail);

			resultSet = preparedStatement.executeQuery();

			while (resultSet.next()) {
				siksinMemberDTO.setMemberNum(resultSet.getInt("memberNum"));
				siksinMemberDTO.setMemberEmail(resultSet.getString("memberEmail"));
				siksinMemberDTO.setPassword(resultSet.getString("password"));
				siksinMemberDTO.setNickName(resultSet.getString("nickName"));
				siksinMemberDTO.setMemberBirth(resultSet.getString("memberBirth"));
				siksinMemberDTO.setGender(resultSet.getString("gender"));
				siksinMemberDTO.setPhoneNum(resultSet.getString("phoneNum"));
				siksinMemberDTO.setMemberArea(resultSet.getString("memberArea"));

			}
		} catch (SQLException e) {
			log.info("DAO_SelectD_개별 회원 조회 실패 - " + e);
		} finally {
			try {
				resultSet.close();
				preparedStatement.close();
				connection.close();
			} catch (SQLException e) {
				e.printStackTrace();
			}
		}
		return siksinMemberDTO;

	}

	@Override
	public SiksinMemberDTO memberEmailcheck(String memberEmail) {

		Connection connection = null;
		PreparedStatement preparedStatement = null;
		ResultSet resultSet = null;
		SiksinMemberDTO siksinMemberDTO = new SiksinMemberDTO();

		try {
			SiksinContext siksinContext = new SiksinContext(); // 내가 만든 연결 클래스를 인스턴스화해야함
			DataSource dataSource = siksinContext.basicDataSource;
			connection = dataSource.getConnection();

			String sql = "select * from siksinMember where memberEmail = ?";

			log.info("DAO_Emailcheck_SQL - " + sql);

			preparedStatement = connection.prepareStatement(sql);
			preparedStatement.setString(1, memberEmail);
			resultSet = preparedStatement.executeQuery();

			if (resultSet.next()) {
				if (resultSet.getString("memberEmail").equals(memberEmail)) {
					siksinMemberDTO.setMemberEmail(resultSet.getString("memberEmail"));
					log.info("DAO_Emailcheck_이메일 확인 - " + resultSet.getString("memberEmail"));
				}
			}

		} catch (Exception e) {
			log.info("DAO_Emailcheck_회원 아이디 체크 실패 - " + e);
		} finally {
			try {
				resultSet.close();
				preparedStatement.close();
				connection.close();
			} catch (SQLException e) {
				e.printStackTrace();
			}
		}
		return siksinMemberDTO;
	}

}

```
<br/>


# dbcp - Context #

```java
package min.java.Siksin.dbcp;

import org.apache.commons.dbcp2.BasicDataSource;

public class SiksinContext {

	public BasicDataSource basicDataSource;

	public SiksinContext() {
		// System.out.println("context 동작");
		basicDataSource = new BasicDataSource();

		basicDataSource.setDriverClassName("oracle.jdbc.driver.OracleDriver");
		basicDataSource.setUrl("jdbc:oracle:thin:@URL주소:1521:xe");
		basicDataSource.setUsername("계정명");
		basicDataSource.setPassword("비밀번호");
		basicDataSource.setInitialSize(4);
		basicDataSource.setMaxIdle(1000);
		basicDataSource.setMinIdle(5);
	}

}

```
<br/>


# control-Select #

```java
package min.java.Siksin.member.control;

import java.util.ArrayList;
import java.util.Scanner;
import org.apache.commons.logging.Log;
import org.apache.commons.logging.LogFactory;
import min.java.Siksin.DAO.SiksinMemberDAO;
import min.java.Siksin.DTO.SiksinMemberDTO;
import min.java.Siksin.action.SiksinMemberAction;

public class SiksinMemberSelect implements SiksinMemberAction {

	private static final Log log = LogFactory.getLog(SiksinMemberSelect.class);

	@Override
	public void execute(Scanner scanner) {
		System.out.println("------ ◆ 회원조회를 선택하였습니다.◆ ------");
		System.out.println("[1] 회원조회  | [2] 회원상세조회");
		System.out.print("◆ 원하는 번호를 입력하세요 : ");
		int choice = scanner.nextInt();
		if (choice == 1) {

			ArrayList<SiksinMemberDTO> arrayList = new ArrayList<SiksinMemberDTO>();
			SiksinMemberDAO siksinMemberDAO = new SiksinMemberDAO();
			arrayList = siksinMemberDAO.SiksinMemberSelectAll();
			log.info("Select데이터 확인 - " + arrayList);
			System.out.println("[회원정보]");

			for (SiksinMemberDTO siksinMemberDTO : arrayList) {
				int memberNum = siksinMemberDTO.getMemberNum();
				String memberEmail = siksinMemberDTO.getMemberEmail();
				String nickName = siksinMemberDTO.getNickName();
				String gender = siksinMemberDTO.getGender();

				System.out.println(
						memberNum + "번" + " | 이메일: " + memberEmail + " | 닉네임: " + nickName + " | 성별: " + gender);
			}

		} else if (choice == 2) {
			SiksinMemberSelectDetail siksinMemberSelectDetail = new SiksinMemberSelectDetail();
			siksinMemberSelectDetail.execute(scanner);
		} else {
			System.out.println("번호를 다시 입력하세요");
			SiksinMemberSelect siksinMemberSelect = new SiksinMemberSelect();
			siksinMemberSelect.execute(scanner);
		}
	}

}

```
<br/>


# control-Insert #

```java
package min.java.Siksin.member.control;

import java.util.ArrayList;
import java.util.Scanner;
import org.apache.commons.logging.Log;
import org.apache.commons.logging.LogFactory;
import min.java.Siksin.DAO.SiksinMemberDAO;
import min.java.Siksin.DTO.SiksinMemberDTO;
import min.java.Siksin.action.SiksinMemberAction;

public class SiksinMemberInsert implements SiksinMemberAction {

	private static final Log log = LogFactory.getLog(SiksinMemberInsert.class);

	@Override
	public void execute(Scanner scanner) {
		System.out.println();
		System.out.println("------ ◆ 회원가입을 선택하였습니다.◆ ------");
		SiksinMemberDAO siksinMemberDAO = new SiksinMemberDAO();
		ArrayList<SiksinMemberDTO> arrayList = new ArrayList<SiksinMemberDTO>();
		
		// 테이블 입력값 조회
		arrayList = siksinMemberDAO.SiksinMemberSelectAll(); 

		System.out.println();
		System.out.println("회원정보를 입력하세요");
		log.info("Insert데이터확인 - " + arrayList);

		if (arrayList.size() >= 0) {

			SiksinMemberDTO siksinMemberDTO = new SiksinMemberDTO();
			System.out.print("이메일: ");
			String memberEmail = scanner.next();
			siksinMemberDTO = siksinMemberDAO.memberEmailcheck(memberEmail);
			System.out.println();
			if (siksinMemberDTO.getMemberEmail() == null) {
				System.out.println("중복된 이메일이 없습니다.");
				siksinMemberDTO = new SiksinMemberDTO();

				System.out.print("비밀번호: ");
				String password = scanner.next();
				System.out.print("닉네임: ");
				String nickName = scanner.next();
				System.out.print("생년월일: ");
				String memberBirth = scanner.next();
				System.out.print("성별(남=m, 여=f): ");
				String gender = scanner.next();
				System.out.print("핸드폰번호: ");
				String phoneNum = scanner.next();
				System.out.print("생활지역: ");
				String memberArea = scanner.next();

				// 자동으로 숫자 저장되게 SQL적어서 안써줘도 됨
//				siksinMemberDTO.setMemberNum(memberNum);
				
				// 입력받은값을  DTO로 저장한다
				siksinMemberDTO.setMemberEmail(memberEmail);
				siksinMemberDTO.setPassword(password);
				siksinMemberDTO.setNickName(nickName);
				siksinMemberDTO.setMemberBirth(memberBirth);
				siksinMemberDTO.setGender(gender);
				siksinMemberDTO.setPhoneNum(phoneNum);
				siksinMemberDTO.setMemberArea(memberArea);// 저장하면서 디티오로 넘어갓따가

				//위에서 저장한 DTO값을 DAO의 인설트매서드로  보내준다.
				siksinMemberDAO.SiksinMemberInsert(siksinMemberDTO);
				System.out.println("'" + nickName + "'" + " 님 회원가입이 완료되었습니다.");
				log.info("Insert회원입력 siksinMemberDTO - " + siksinMemberDTO); // 여기서 저장된 데이터 확인을 위해 get으로 불러와서 확인한다.
				return;
				
			} else {
				System.out.println("중복된 이메일이 있습니다. 다시 입력하세요.");
				log.info("Insert중복 아이디 확인 - " +siksinMemberDTO.getMemberEmail().equals(memberEmail));
				System.out.println();
			}
		}
	}
}

```
<br/>


# control-Update #

```java
package min.java.Siksin.member.control;

import java.util.ArrayList;
import java.util.Scanner;
import org.apache.commons.logging.Log;
import org.apache.commons.logging.LogFactory;
import min.java.Siksin.DAO.SiksinMemberDAO;
import min.java.Siksin.DTO.SiksinMemberDTO;
import min.java.Siksin.action.SiksinMemberAction;

public class SiksinMemberUpdate implements SiksinMemberAction {

	private static final Log log = LogFactory.getLog(SiksinMemberUpdate.class);

	@Override
	public void execute(Scanner scanner) {
		System.out.println();
		System.out.println("------ ◆ 회원정보 수정을 선택하였습니다.◆ ------");

		SiksinMemberDAO siksinMemberDAO = new SiksinMemberDAO();
		ArrayList<SiksinMemberDTO> arrayList = new ArrayList<SiksinMemberDTO>();
		arrayList = siksinMemberDAO.SiksinMemberSelectAll();
		System.out.println("회원정보를 수정하세요");

		for (SiksinMemberDTO siksinMemberDTO : arrayList) {
			System.out.print("회원 이메일: ");
			String memberEmail = scanner.next();
			
			siksinMemberDTO = siksinMemberDAO.memberEmailcheck(memberEmail);
			
			System.out.println(siksinMemberDTO);
			System.out.println();
			if (siksinMemberDTO.getMemberEmail() == null) {
				System.out.println("이메일이 없습니다. 다시 입력하세요.");
			} else {
				log.info("Update이메일 확인 - " + siksinMemberDTO.getMemberEmail().equals(memberEmail));
				System.out.println();
				System.out.println("이메일이 있습니다. 회원정보수정을 진행해주세요.");
				siksinMemberDTO = siksinMemberDAO.SiksinMemberSelectD(memberEmail);
				log.info("Update회원정보siksinMemberDTO" + siksinMemberDTO);
				System.out.println("[회원정보 수정]");
				System.out.println("비밀번호: " + siksinMemberDTO.getPassword());
				System.out.print("수정할 비밀번호: ");
				String password = scanner.next();
				System.out.println("닉네임: " + siksinMemberDTO.getNickName());
				System.out.print("수정할 닉네임: ");
				String nickName = scanner.next();
				System.out.println("핸드폰번호: " + siksinMemberDTO.getPhoneNum());
				System.out.print("수정할 핸드폰번호: ");
				String phoneNum = scanner.next();
				System.out.println("생활지역:" + siksinMemberDTO.getMemberArea());
				System.out.print("수정할 생활지역: ");
				String memberArea = scanner.next();
				
				siksinMemberDTO.setMemberEmail(memberEmail);
				siksinMemberDTO.setPassword(password);
				siksinMemberDTO.setNickName(nickName);
				siksinMemberDTO.setPhoneNum(phoneNum);
				siksinMemberDTO.setMemberArea(memberArea);
//				System.out.println(siksinMemberDTO);
				siksinMemberDAO.SiksinMemberUpdate(memberEmail, password, nickName, phoneNum, memberArea);
				System.out.println(nickName + " 님의 회원정보가 수정되었습니다.");
				log.info("Update회원수정siksinMemberDTO " + siksinMemberDTO);
				break;
			}

		}
	}
}

```
<br/>


# control-Delete #

```java
package min.java.Siksin.member.control;

import java.util.ArrayList;
import java.util.Scanner;
import org.apache.commons.logging.Log;
import org.apache.commons.logging.LogFactory;
import min.java.Siksin.DAO.SiksinMemberDAO;
import min.java.Siksin.DTO.SiksinMemberDTO;
import min.java.Siksin.action.SiksinMemberAction;

public class SiksinMemberDelete implements SiksinMemberAction {
	private static final Log log = LogFactory.getLog(SiksinMemberDelete.class);

	@Override
	public void execute(Scanner scanner) {
		System.out.println();
		System.out.println("------ ◆ 회원정보 삭제을 선택하였습니다.◆ ------");
		SiksinMemberDAO siksinMemberDAO = new SiksinMemberDAO();
		ArrayList<SiksinMemberDTO> arrayList = new ArrayList<SiksinMemberDTO>();
		arrayList = siksinMemberDAO.SiksinMemberSelectAll();
		System.out.println("삭제할 이메일을 입력해주세요.");

		for (SiksinMemberDTO siksinMemberDTO : arrayList) {
			System.out.print("회원 이메일: ");
			String memberEmail = scanner.next();

			siksinMemberDTO = siksinMemberDAO.memberEmailcheck(memberEmail);

			if (siksinMemberDTO.getMemberEmail() == null) {
				System.out.println("삭제할 회원이 없습니다.");
			} else {
				log.info("Delete아이디 확인 - " + siksinMemberDTO.getMemberEmail().equals(memberEmail));
				System.out.println("삭제할 회원이 있습니다.");

				System.out.print("회원에서 탈퇴하시겠습니까(y/n) : ");
				String choice = scanner.next();
				switch (choice) {
				case "y":
					siksinMemberDAO.SiksinMemberDelete(memberEmail);
					System.out.println("회원정보가 삭제되었습니다.");
					break;
				case "n":
					System.out.println("내용을 취소합니다.");
					break;
				default:
					System.out.println("잘못입력하였습니다.");
					break;
				}
			}
			break;
		}
	}
}

```
<br/>



# control-SelectDetail #

```java
package min.java.Siksin.member.control;

import java.util.Scanner;
import org.apache.commons.logging.Log;
import org.apache.commons.logging.LogFactory;
import min.java.Siksin.DAO.SiksinMemberDAO;
import min.java.Siksin.DTO.SiksinMemberDTO;
import min.java.Siksin.action.SiksinMemberAction;

public class SiksinMemberSelectDetail implements SiksinMemberAction {

	private static final Log log = LogFactory.getLog(SiksinMemberSelectDetail.class);

	@Override
	public void execute(Scanner scanner) {

		do {
			SiksinMemberDTO siksinMemberDTO = new SiksinMemberDTO();
			SiksinMemberDAO siksinMemberDAO = new SiksinMemberDAO();
			System.out.println("------ ◆ 회원정보 상세보기를 선택하였습니다.◆ ------");
			System.out.print("회원 이메일: ");
			String memberEmail = scanner.next();

			siksinMemberDTO = siksinMemberDAO.SiksinMemberSelectD(memberEmail);

			int memberNum = siksinMemberDTO.getMemberNum();
			memberEmail = siksinMemberDTO.getMemberEmail();
			String password = siksinMemberDTO.getPassword();
			String nickName = siksinMemberDTO.getNickName();
			String memberBirth = siksinMemberDTO.getMemberBirth();
			String gender = siksinMemberDTO.getGender();
			String phoneNum = siksinMemberDTO.getPhoneNum();
			String memberArea = siksinMemberDTO.getMemberArea();

			if (siksinMemberDTO.getMemberEmail() == null) {
				System.out.println();
				System.out.println("존재하는 회원이 없습니다.");

			} else {
				log.info("SelectDetail아이디 확인 - " + siksinMemberDTO.getMemberEmail().equals(memberEmail));
				System.out.println("---------------------------");
				System.out.println("회원번호	: " + memberNum);
				System.out.println("이메일	: " + memberEmail);
				System.out.println("비밀번호	: " + password);
				System.out.println("닉네임	: " + nickName);
				System.out.println("생년월일	: " + memberBirth);
				System.out.println("성별	: " + gender);
				System.out.println("핸드폰번호	: " + phoneNum);
				System.out.println("생활지역	: " + memberArea);
				System.out.println("---------------------------");
				return;

			}
		} while (true);

	}
}

```
<br/>


# view-Main #

```java
package min.java.Siksin.view;

import java.util.Scanner;

import min.java.Siksin.member.control.SiksinMemberDelete;
import min.java.Siksin.member.control.SiksinMemberInsert;
import min.java.Siksin.member.control.SiksinMemberSelect;
import min.java.Siksin.member.control.SiksinMemberUpdate;

public class SiksinMemberMain {
	public static void main(String[] args) {

		Scanner scanner = new Scanner(System.in);

		do {
			System.out.println();
			System.out.println(
					"------------------------------------------ <식신> ------------------------------------------");
			System.out.println(
					"------------------------------------ 대한민국 NO.1 맛집 서비스  -----------------------------------");
			System.out.println("[회원정보]");
			System.out.println("[1] 회원조회  | [2] 회원가입 | [3] 회원수정 | [4] 회원정보삭제 | [5] 회원정보 페이지 종료");
			System.out.print("◆ 원하는 번호를 입력하세요 : ");
			String choice = scanner.next();

			switch (choice) {
			case "1":
				SiksinMemberSelect siksinMemberSelect = new SiksinMemberSelect();
				siksinMemberSelect.execute(scanner);
				break;
			case "2":
				SiksinMemberInsert siksinMemberInsert = new SiksinMemberInsert();
				siksinMemberInsert.execute(scanner);
				break;
			case "3":
				SiksinMemberUpdate siksinMemberUpdate = new SiksinMemberUpdate();
				siksinMemberUpdate.execute(scanner);
				break;
			case "4":
				SiksinMemberDelete siksinMemberDelete = new SiksinMemberDelete();
				siksinMemberDelete.execute(scanner);
				break;
			case "5":
				System.out.println("프로그램을 종료합니다.");
				System.exit(0);
			default:

				break;
			}

		} while (true);
	}
}

```
<br/>


# dbconnection - ConnectionDB #

```java
package min.java.Siksin.dbconnection.test;

import java.sql.Connection;
import java.sql.SQLException;
import javax.sql.DataSource;
import org.apache.commons.logging.Log;
import org.apache.commons.logging.LogFactory;
import min.java.Siksin.dbcp.SiksinContext;

public class SiksinConnectionDB {

	private static final Log log = LogFactory.getLog(SiksinConnectionDB.class);

	public static void main(String[] args) {
		Connection connection = null;

		try {
			SiksinContext siksinContext = new SiksinContext();
			DataSource dataSource = siksinContext.basicDataSource;
			connection = dataSource.getConnection();
			log.info("ConnectionDB데이터베이스 연결 - " + connection);

		} catch (SQLException e) {
			log.info("ConnectionDB데이터베이스 연결 실패 - " + e);
		} finally {
			try {
				connection.close();
			} catch (Exception e) {
				e.printStackTrace();
			}
		}
	}
}
```
<br/>