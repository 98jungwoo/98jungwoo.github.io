---
layout: single
title:  "[Java] 로그인, 종합페이지 개발 3(MVC)"
categories: Java-개발
toc: true
---

![로그인,종합페이지](https:/images/2023-04-01-development/로그인,종합페이지.JPG)


# 로그인 # 

```java
package min.login.control;

import java.util.Scanner;
import min.intro.view.QIntroMain;
import min.member.command.MemberCommand;
import min.member.control.MemberAction;
import min.member.service.MemberInsert;

public class QMemberLogin implements MemberAction {

	@Override
	public MemberCommand start(Scanner scanner) {
		System.out.println();
		System.out.println("------ Login ------");

		MemberCommand memberCommand = new MemberCommand();

		// 아이디와 비밀번호 입력
		if (arrayList.size() > 0) {
			int index = -1;
			System.out.print("◆ ID 입력 : ");
			String id = scanner.next();
			System.out.print("◆ PassWord 입력 : ");
			String password = scanner.next();

			// 사전에 입력한 내용이 있는지 확인
			for (int i = 0; i < arrayList.size(); i++) {

				if (id.equals(arrayList.get(i).getId()) & password.equals(arrayList.get(i).getPassword())) {
					index = i;
					System.out.println();
					System.out.println(arrayList.get(i).getNickname() + "님 반갑습니다! 로그인에 성공하였습니다.");
					System.out.println();
					QIntroMain.main(null);
					break;
				}
			}

			// 아이디와 비번을 틀리게 입력하면(=index가 변경되지 않았다면) 일지하지 않는다고 나온다.
			if (index == -1) {
				System.out.println("ID와 Password가 일치하지 않습니다.");
			}

			// 어레이 리스트에 등록한 내용이 있다면 위에 내용을 실행시키고, 등록된 내용이 없으면 회원가입을 하라고 물어본다.
		} else {
			System.out.println("등록된 회원정보가 없습니다.");

			System.out.print("회원가입을 진행하시겠습니까?(y/n) : ");
			String yn = scanner.next();

			switch (yn) {
			case "y":
				MemberInsert memberInsert = new MemberInsert();
				memberInsert.start(scanner);
				break;
			case "n":
				QIntroMain.main(null);
				break;

			default:
				System.out.println("잘못 입력하셨습니다.");
				break;
			}
		}
		return memberCommand;
	}
}

```

# 종합페이지 #

```java
package min.intro.view;

import java.util.Scanner;

import min.board.view.BoardMain;
import min.login.control.QMemberLogin;
import min.member.service.MemberInsert;
import min.member.view.MemberMain;

public class QIntroMain {
	public static void main(String[] args) {
		Scanner scanner = new Scanner(System.in);

		do {
			System.out.println();
			System.out.println("------------------ <식신> ------------------");
			System.out.println("------ 대한민국 NO.1 맛집 서비스 ------");
			System.out.println();
			System.out.println("[1] 로그인 | [2] 회원가입 | [3] 회원관리 | [4] 리뷰 관리 | [5] 홈페이지 종료");
			System.out.print("◆ 원하시는 번호를 입력하세요 : ");

			String ch = scanner.next();
			switch (ch) {
			case "1":
				QMemberLogin qMemberLogin = new QMemberLogin();
				qMemberLogin.start(scanner);
				break;
			case "2":
				MemberInsert memberInsert = new MemberInsert();
				memberInsert.start(scanner);
				break;
			case "3":
				MemberMain.main(null);
				break;
			case "4":
				BoardMain.main(null);
				break;
			case "5":
				System.out.println("식신: 맛집서비스 홈페이지를 종료합니다.");
				System.out.println("------ The End ------");
				System.exit(0);
			default:
				System.out.println("번호를 잘못 입력하였습니다. 다시 입력해주세요.");
				break;
			}
		} while (true);
	}
}

```


