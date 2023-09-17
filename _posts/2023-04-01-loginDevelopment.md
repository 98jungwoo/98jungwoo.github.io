---
layout: single
title:  "[Java] 회원가입 개발 1(MVC)"
categories: Java
toc: true
---
<br/><br/>

[[Java] 개발의 기본순서는 (분석 - 설계 - 코딩)이다.](https://98jungwoo.github.io/java/development/)

위에 포스팅에서 개발을 할때 순서를 지키면서 해야한다는 내용을 다룬적이 있다.

내용을 지키면서 또 알아야할 내용을 이야기하고 간단한 회원가입, 로그인, 게시판을 공유하도록 한다.(본 코드는 데이터베이스와 아직 연동하지 않았으며, 이클립스에서 실행 하여 확인할 수 있는 회원가입, 로그인, 게시판이다.)
<br/><br/>

# 다이어그램 #

![개발다이어그램](https:/images/2023-04-01-development/개발다이어그램.JPG)

위의 그림은 CRUD의 개발의 흐름을 보여주는 다이어그램이다.

입력view - Controller - Command - Service(CRUD) - Command - DAO - Oracle - DAO - command - Controller - 출력view

이런 형태의 흐름으로 진행이된다.
<br/><br/>

![회원가입패키지,클래스](https:/images/2023-04-01-development/회원가입패키지클래스.JPG)
<br/>

```java
package min.member.command;

public class MemberCommand {

	private String id;
	private String password;
	private String name;
	private String nickname;
	private int birth;

	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	public String getId() {
		return id;
	}

	public void setId(String id) {
		this.id = id;
	}

	public String getPassword() {
		return password;
	}

	public String getNickname() {
		return nickname;
	}

	public void setNickname(String nickname) {
		this.nickname = nickname;
	}

	public void setPassword(String password) {
		this.password = password;
	}

	public int getBirth() {
		return birth;
	}

	public void setBirth(int birth) {
		this.birth = birth;
	}

	@Override
	public String toString() {
		return "MemberCommand [id=" + id + ", password=" + password + ", name=" + name + ", nickname=" + nickname
				+ ", birth=" + birth + "]";
	}

}
```


```java
package min.member.control;

import java.util.ArrayList;
import java.util.Scanner;

import min.member.command.MemberCommand;

public interface MemberAction {
	ArrayList<MemberCommand> arrayList = new ArrayList<MemberCommand>();
	
	public MemberCommand start(Scanner scanner);
}
```


```java
package min.member.view;

import java.util.Scanner;
import min.intro.view.QIntroMain;
import min.member.service.*;

public class MemberMain {
	public static void main(String[] args) {

		Scanner scanner = new Scanner(System.in);

		do {
			System.out.println();
			System.out.println("------ 회원관리 ------");
			System.out.println("[1] 전체회원 보기 | [2]  회원가입 | [3] 회원정보 수정 | [4] 회원삭제 | [5] 프로그램 종료");
			System.out.print("◆ 원하시는 번호를 선택해주세요 : ");

			String choice = scanner.next();
			switch (choice) {

			case "1":
				MemberSelect memberSelect = new MemberSelect();
				memberSelect.start(scanner);
				break;
			case "2":
				MemberInsert memberInsert = new MemberInsert();
				memberInsert.start(scanner);
				break;
			case "3":
				MemberUpdate memberUpdate = new MemberUpdate();
				memberUpdate.start(scanner);
				break;
			case "4":
				MemberDelete memberDelete = new MemberDelete();
				memberDelete.start(scanner);
				break;
			case "5":
				System.out.println();
				System.out.println("회원관리를 종료합니다.");
//			System.out.println("------ The End ------");
//			System.exit(0);
				QIntroMain.main(null);

			default:
				System.out.println("번호를 다시 입력해주세요. ");
				System.out.println();
				break;
			}
		} while (true);
	}
}

```


```java
package min.member.service;

import java.util.Scanner;

import min.member.command.MemberCommand;
import min.member.control.MemberAction;

public class MemberSelect implements MemberAction {

	@Override
	public MemberCommand start(Scanner scanner) {
		System.out.println("------ 전체회원 보기를 선택하였습니다. ------");

		if (arrayList.size() > 0) {

			for (int i = 0; i < arrayList.size(); i++) {
				System.out.println("◆ ID : " + arrayList.get(i).getId() + ", ");
				System.out.println("◆ PassWord : " + arrayList.get(i).getPassword() + ", ");
				System.out.println("◆ 이름 : "+ arrayList.get(i).getName() + ", ");
				System.out.println("◆ 생년월일 : " + arrayList.get(i).getBirth());
				System.out.println("◆ 닉네임 : " + arrayList.get(i).getNickname());
				System.out.println();

			}
		} else {
			System.out.println("회원정보가 없습니다. [2]번을 입력해서 추가해주세요.");
			System.out.println();
		}
		return null;
	}
}

```


```java
package min.member.service;

import java.util.Scanner;

import min.member.command.MemberCommand;
import min.member.control.MemberAction;
import min.member.view.MemberMain;

public class MemberInsert implements MemberAction {

	@Override
	public MemberCommand start(Scanner scanner) {
		System.out.println();
		System.out.println("------ 회원가입을 선택하였습니다. ------");
		int birth;

		if (arrayList.size() >= 0) {
			System.out.print("◆ ID 입력 : ");
			String id = scanner.next();

			for (int i = 0; i < arrayList.size(); i++) {

				if (id.equals(arrayList.get(i).getId())) {
					System.out.println("다른 사용자가 ID를 사용중입니다. 다시 작성해주세요.");
					MemberMain.main(null);
				}
			}

			String password2;
			System.out.print("◆ PassWord 입력 : ");
			String password = scanner.next();

			do {
				System.out.println("비밀번호를 한번 더 입력하세요");
				System.out.print("◆ PassWord 입력 : ");
				password2 = scanner.next();
			} while (!password.equals(password2));

			System.out.print("◆ 이름 입력 : ");
			String name = scanner.next();

			int number;
			do {
				System.out.print("◆ 생년월일 입력(8자리 숫자 입력 ex) 19980421) : ");
				birth = scanner.nextInt();

				// 내가 입력한 자리수 계산하기위한 식
				number = (int) (Math.log10(birth) + 1); 

			} while (number != 8);// 자리수가 8이되면 반복을 그만둬

			System.out.print("◆ 닉네임 입력 : ");
			String nikname = scanner.next();

			MemberCommand memberCommand = new MemberCommand();
			memberCommand.setId(id);
			memberCommand.setPassword(password);
			memberCommand.setName(name);
			memberCommand.setNickname(nikname);
			memberCommand.setBirth(birth);

			arrayList.add(memberCommand);
			System.out.println();
			System.out.println("반갑습니다. " + nikname + " 님! 회원가입이 완료되었습니다.");

			//
			return memberCommand;// 이러면 커맨드 2를 데이터베이스에 보내줄수가 없지
		}

		return null;
	}
}
```


```java
package min.member.service;

import java.util.Scanner;
import min.member.command.MemberCommand;
import min.member.control.MemberAction;

public class MemberUpdate implements MemberAction {

	@Override
	public MemberCommand start(Scanner scanner) {
		System.out.println("------ 회원정보 수정을 선택하였습니다. ------");

		if (arrayList.size() > 0) {
			int index = -1;

			System.out.print("◆ ID 입력 : ");
			String id = scanner.next();
			System.out.println();

			for (int i = 0; i < arrayList.size(); i++) {
				if (id.equals(arrayList.get(i).getId())) {
					index = i;
					arrayList.remove(i);
				}
			}

			if (index == -1) {
				System.out.println("등록된 ID가 없습니다. 다시한번 확인해주세요.");
			} else {
				System.out.println("------ 회원정보를 수정하세요. ------");
				System.out.println("◆ ID 입력 : " + id);
				System.out.print("◆ PassWord 입력 : ");
				String password = scanner.next();
				System.out.print("◆ 이름 입력 : ");
				String name = scanner.next();
				System.out.print("◆ 닉네임 입력 : ");
				String nikname = scanner.next();
				System.out.print("◆ 생년월일 입력(6자리 숫자 입력 ex) 980421) : ");
				int birth = scanner.nextInt();



				System.out.println("------ 수정 할 정보 ------");
				System.out.println("◆ ID : " + id);
				System.out.println("◆ PassWord : " + password);
				System.out.println("◆ 이름 : " + name);
				System.out.println("◆ 닉네임 : " + nikname);
				System.out.println("◆ 생년월일 :" + birth);


				System.out.print("확인한 정보가 맞습니까? (y/n): ");
				String cho = scanner.next();

				MemberCommand memberCommand = new MemberCommand();

				switch (cho) {
				case "y":
		    	    memberCommand.setId(id);
		        	memberCommand.setPassword(password);
		        	memberCommand.setName(name);
		        	memberCommand.setNickname(nikname);
		        	memberCommand.setBirth(birth);

					System.out.println();
					System.out.println("수정이 완료되었습니다.");
					arrayList.add(memberCommand);
					break;
				case "n":
					System.out.println("회원정보 수정을 다시 진행해 주세요.");
					break;

				default:
					break;
				}

				return memberCommand;
			}
		} else {
			System.out.println("회원정보가 없습니다. [2]번을 입력해서 추가해주세요.");
		}
		return null;
	}
}

```


```java
package min.member.service;

import java.util.Scanner;
import min.member.command.MemberCommand;
import min.member.control.MemberAction;

public class MemberDelete implements MemberAction {

	@Override
	public MemberCommand start(Scanner scanner) {

		System.out.println("------ 회원삭제를 선택하였습니다. ------");

		if (arrayList.size() > 0) {
			int index = -1;
			System.out.print("◆ ID 입력 : ");
			String id = scanner.next();

			for (int i = 0; i < arrayList.size(); i++) {

				if (id.equals(arrayList.get(i).getId())) {// == 주소값 확인 // equals는 실제값 확인(외부에서는 equals쓴다.)
					index = i;
					arrayList.remove(i);
					System.out.println("회원정보가 삭제 되었습니다.");
					System.out.println();
				}
			}

			if (index == -1) {
				System.out.println("ID가 일치하지 않습니다. 다시 입력해주세요.");

			} else {
				System.out.println("회원정보가 없습니다.");

			}
		}
		return null;
	}
}
```

