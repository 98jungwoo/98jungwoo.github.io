---
layout: single
title:  "[Java] 게시판 개발 2"
categories: Java-개발
toc: true
---
<br/><br/>

![게시판패키지,클래스](https:/images/2023-04-01-development/보드패키지클래스.JPG)
<br/>

```java
package min.board.command;

public class BoardCommand {

	private int num;
	private String id;
	private int password;
	private String title;
	private String contents;

	public int getNum() {
		return num;
	}

	public void setNum(int num) {
		this.num = num;
	}

	public String getId() {
		return id;
	}

	public void setId(String id) {
		this.id = id;
	}

	public int getPassword() {
		return password;
	}

	public void setPassword(int password) {
		this.password = password;
	}

	public String getTitle() {
		return title;
	}

	public void setTitle(String title) {
		this.title = title;
	}

	public String getContents() {
		return contents;
	}

	public void setContents(String contents) {
		this.contents = contents;
	}

	@Override
	public String toString() {
		return "MemberCommand [num=" + num + ", id=" + id + ", password=" + password + ", title=" + title
				+ ", contents=" + contents + "]";
	}

}
```

```java
package min.board.control;

import java.util.ArrayList;
import java.util.Scanner;

import min.board.command.boardCommand;

public interface BoardAction {
	ArrayList<BoardCommand> arrayList = new ArrayList<BoardCommand>();

	public BoardCommand start(Scanner scanner);
}
```

```java
package min.board.view;

import java.util.Scanner;
import min.board.service.*;


public class BoardMain {
	public static void main(String[] args) {

		Scanner scanner = new Scanner(System.in);

		do {
			System.out.println("------ 게시판 ------");
			System.out.println("[1] 전체게시글 보기 | [2] 게시글등록 | [3] 내용수정 | [4] 게시글삭제 | [5] 프로그램 종료");
			System.out.print("◆ 원하시는 번호를 선택해주세요 : ");

			String choice = scanner.next();

			switch (choice) {
			case "1":
				BoardSelect memberSelect = new BoardSelect();
				memberSelect.start(scanner);
				break;
			case "2":
				BoardInsert memberInsert = new BoardInsert();
				memberInsert.start(scanner);
				break;
			case "3":
				BoardUpdate memberUpdate = new BoardUpdate();
				memberUpdate.start(scanner);
				break;
			case "4":
				BoardDelete memberDelete = new BoardDelete();
				memberDelete.start(scanner);
				break;
			case "5":
				System.out.println("프로그램을 종료합니다.");
				System.out.println("------ The End ------");
				System.exit(0);

			default:
				System.out.println("번호를 다시 입력해주세요. ");
				break;
			}
		} while (true);
	}
}
```

```java
package min.board.service;

import java.util.Scanner;
import min.board.command.boardCommand;
import min.board.control.boardAction;

public class BoardSelect implements BoardAction {

	@Override
	public BoardCommand start(Scanner scanner) {
		System.out.println("------ 전체게시글 보기를 선택하였습니다. ------");

		if (arrayList.size() > 0) {

			for (int i = 0; i < arrayList.size(); i++) {

				System.out.println("◆ 게시글 번호 : " + arrayList.get(i).getNum() + ", ");
				System.out.println("◆ ID : " + arrayList.get(i).getId() + ", ");
				System.out.println("◆ PassWord : " + arrayList.get(i).getPassword() + ", ");
				System.out.println("◆ 제목 : " + arrayList.get(i).getTitle() + ", ");
				System.out.println("◆ 내용 입력 : " + arrayList.get(i).getContents());
				System.out.println();

			}
		} else {
			System.out.println("게시글이 없습니다. [2]번을 입력해서 추가해주세요.");
			System.out.println();
		}

		return null;
	}

}
```

```java
package min.board.service;

import java.util.Scanner;
import min.board.command.boardCommand;
import min.board.control.boardAction;
import min.board.view.boardMain;

public class BoardInsert implements BoardAction {

	@Override
	public BoardCommand start(Scanner scanner) {

		System.out.println("------ 게시글 등록을 선택하였습니다. ------");

		if (arrayList.size() >= 0) {
			System.out.print("◆ 게시글 번호 입력 : ");
			int num = scanner.nextInt();

			for (int i = 0; i < arrayList.size(); i++) {

				if (num == arrayList.get(i).getNum()) {
					System.out.println("같은 게시글 번호가 있습니다.");
					BoardMain.main(null);// ?
				}
			}

			System.out.print("◆ ID 입력 : ");
			String id = scanner.next();

			System.out.print("◆ PassWord 입력 : ");
			int password = scanner.nextInt();

			System.out.print("◆ 제목 입력 : ");
			String title = scanner.next();

			System.out.print("◆ 내용 입력 : ");
			String contents = scanner.next();

			BoardCommand memberCommand = new BoardCommand();
			memberCommand.setNum(num);
			memberCommand.setId(id);
			memberCommand.setPassword(password);
			memberCommand.setTitle(title);
			memberCommand.setContents(contents);

			arrayList.add(memberCommand);
			System.out.println("게시글 등록이 완료되었습니다.");
			System.out.println();
			return memberCommand;
		}
		return null;
	}
}
```

```java
package min.board.service;

import java.util.Scanner;
import min.board.command.boardCommand;
import min.board.control.boardAction;

public class BoardUpdate implements BoardAction {

	@Override
	public BoardCommand start(Scanner scanner) {
		System.out.println("------ 게시글 수정을 선택하였습니다. ------");

		if (arrayList.size() > 0) {
			int index = -1;
			System.out.println("◆ 게시글 번호 입력 : ");
			int num = scanner.nextInt();
			System.out.println();

			for (int i = 0; i < arrayList.size(); i++) {
				if (num == arrayList.get(i).getNum()) {
					index = i;
					arrayList.remove(i);
				}
			}

			if (index == -1) {
				System.out.println("등록된 게시글이 없습니다. 다시한번 확인해주세요.");
			} else {
				System.out.println("------ 게시글을 수정하세요. ------");

				System.out.println("◆ 게시글 번호 입력 :  " + num);

				System.out.print("◆ ID 입력 : ");
				String id = scanner.next();

				System.out.print("◆ PassWord 입력 : ");
				int password = scanner.nextInt();

				System.out.print("◆ 제목 입력 : ");
				String title = scanner.next();

				System.out.print("◆ 내용 입력");
				String contents = scanner.next();

				BoardCommand memberCommand = new BoardCommand();
				memberCommand.setNum(num);
				memberCommand.setId(id);
				memberCommand.setPassword(password);
				memberCommand.setTitle(title);
				memberCommand.setContents(contents);

				arrayList.add(memberCommand);
				System.out.println("게시글 수정이 완료되었습니다.");
				System.out.println();

				return memberCommand;
			}
		} else {
			System.out.println("게시글이 없습니다. [2]번을 입력해서 추가해주세요.");

		}
		return null;
	}
}
```

```java
package min.board.service;

import java.util.Scanner;
import min.board.command.boardCommand;
import min.board.control.boardAction;

public class BoardDelete implements BoardAction {

	@Override
	public BoardCommand start(Scanner scanner) {

		System.out.println("------ 게시글 삭제을 선택하였습니다. ------");

		if (arrayList.size() > 0) {
			int index = -1;
			System.out.print("◆ 게시글 번호 입력 : ");
			int num = scanner.nextInt();

			for (int i = 0; i < arrayList.size(); i++) {

				if (num == arrayList.get(i).getNum()) {// == 주소값 확인 // equals는 실제값 확인(외부에서는 이퀄쓴다.)
					//
					index = i;
					arrayList.remove(i);
					System.out.println("게시글이 삭제 되었습니다.");
					System.out.println();
				}
			}

			if (index == -1) {
				System.out.println("번호를 다시한번 확인해주세요.");

			} else {
				System.out.println("등록된 게시글이 없습니다.");

			}
		}
		return null;
	}
}
```