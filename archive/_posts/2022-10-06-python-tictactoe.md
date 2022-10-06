---
layout: post
title: <Python> 틱택토 게임 구현
description: >
  python으로 틱택토 게임 구현하기, class 객체 사용하기
sitemap: false
hide_last_modified: true
---

틱택토 게임을 구현해봤다. 파이썬은 C/C++에 비해서 문자열 비교가 너무 쉬워서 너무 행복하다.

~~~python
### 22.10.06
### 틱택토 게임 구현
### class 변환해서 구현

import time


class TicTacToe:
    def __init__(self):
        self.board = {(i + 1): " " for i in range(9)}
        self.turn = 0
        self.player = "B"
        self.markers = {"A": "X", "B": "O"}

    def print_board(self):
        print("")
        for i in range(1, 10):
            print(f"{i}: {self.board[i]} ", end=" ")
            if i % 3 == 0:
                print("")

    #####################
    ### player 전환
    def next_player(self):
        if self.turn % 2 == 0:  # A 차례
            return "A"
        else:
            return "B"

    ######################
    ### input 관리
    def insert_input(self, player, marker):
        input_slot = int(input(f"{player} >> marker({marker}) 표시 위치를 선택하세요(1~9): "))

        while input_slot < 1 or input_slot > 9 or self.board[input_slot] != " ":
            input_slot = int(input(f"{player} >> 적절한 범위와 빈 슬롯의 번호를 다시 입력하세요(1~9): "))

        self.board[input_slot] = marker
        self.turn += 1

    ################
    ### 승패 결정: 승부가 끝났다면 True 반환
    def win_game(self):
        # 세로
        for start in range(1, 4):
            if self.board[start] != " " and self.board[start] == self.board[start + 3] == self.board[start + 6]:
                return True
        # 가로
        for start in range(1, 9, 3):
            if self.board[start] != " " and self.board[start] == self.board[start + 1] == self.board[start + 2]:
                return True

        # 대각선
        if self.board[5] != " " and \
                (self.board[1] == self.board[5] == self.board[9] or self.board[3] == self.board[5] == self.board[7]):
            return True

    ################
    ### 게임을 더 할 건지
    def play_again(self):
        c = input(f"New game? (y/n): ")
        if c == "y":
            self.__init__()
            return True
        else:
            return False

    ################
    ### 메인 게임 실행 함수
    def game(self):
        cont = True # continue game?

        while cont:
            self.print_board()
            self.player = self.next_player()  # self.count 기준으로 다음 순서 정하기

            ### marker 위치 input 받기
            self.insert_input(self.player, self.markers[self.player])

            ### 승패 판정
            res = self.win_game()

            ### 게임 끝, 다음 게임 진행 여부
            if res:
                self.print_board()
                time.sleep(0.5)
                print(f"{self.player} WIN -------------------\n")
                cont = self.play_again()  # 새로운 게임

            if not res and self.turn == 9:  # 무승부 판정
                time.sleep(0.5)
                print(f"TIE GAME -----------\n")
                cont = self.play_again()  # 새로운 게임


ttt = TicTacToe()
ttt.game()
~~~