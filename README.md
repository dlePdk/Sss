#include <stdio.h>

// 전역 변수: 단서 획득 여부 표시 (1 = 획득)
int clue_phone = 0;
int clue_article = 0;
int clue_prescription = 0;
int clue_original_article = 0;
int clue_diary = 0;
int clue_medicine = 0;

// 함수 선언
void intro();
void day1();
void day2();
void analyze();
void ending();

int main() {
    intro();
    day1();
    day2();
    analyze();
    ending();
    return 0;
}

void intro() {
    printf("《그리고 진실은 하나뿐이었다》\n");
    printf("외딴섬에 초대된 네 명의 인물...\n");
    printf("정체불명의 편지, 불러낸 이는 없고...\n\n");

    printf("등장인물 소개\n\n");

    printf("[이수아] - 고등학생 (플레이어)\n");
    printf("조용하지만 관찰력이 뛰어난 소녀. 이번 사건의 중심에 서게 된다.\n\n");

    printf(" [한지우] - 의사\n");
    printf("차분하고 말수가 적은 인물. 과거 환자의 죽음을 숨긴 의혹이 있다.\n\n");

    printf("[박서진] - 기자\n");
    printf("냉철한 시선과 날카로운 언변을 지닌 인물. 기사로 누군가를 파멸시킨 과거가 있다.\n\n");

    printf("[최윤호] - 사업가\n");
    printf("겉으론 유쾌하지만 어딘가 이중적인 태도. 뇌물과 협박의 흔적이 있다.\n\n");

    printf("밤이 깊어가고, 모두는 불안한 얼굴로 각자의 방으로 향한다...\n\n");
}

void day1() {
    int choice;
    printf("Day 1: 최윤호가 사망한 채 발견됐다.\n");
    printf("1. 최윤호 방 조사\n");
    printf("2. 거실 서재 탐색\n");
    printf("3. 한지우와 대화\n");
    printf("선택: ");
    scanf("%d", &choice);

    switch(choice) {
        case 1:
            printf("휴대폰에서 협박 문자를 발견했다.\n");
            clue_phone = 1;
            break;
        case 2:
            printf("찢어진 신문 기사 조각을 발견했다.\n");
            clue_article = 1;
            break;
        case 3:
            printf("한지우가 진통제 처방 기록을 숨겼다는 걸 알게 됐다.\n");
            clue_prescription = 1;
            break;
        default:
            printf("잘못된 입력입니다. 아무 일도 일어나지 않았다.\n");
            break;
    }
    printf("\n");
}

void day2() {
    int choice, count = 0;
    printf("Day 2: 추가 조사를 할 수 있다. 최대 2개 선택 가능.\n");
    while(count < 2) {
        printf("1. 박서진 방 수색\n");
        printf("2. 피해자 일기장 발견\n");
        printf("3. 의료 상자 조사\n");
        printf("4. 조사 종료\n");
        printf("선택: ");
        scanf("%d", &choice);

        if(choice == 4) {
            printf("조사를 종료합니다.\n");
            break;
        }

        switch(choice) {
            case 1:
                if(clue_original_article == 0) {
                    printf("내부고발 기사 원본을 발견했다.\n");
                    clue_original_article = 1;
                    count++;
                } else {
                    printf("이미 조사한 항목입니다.\n");
                }
                break;
            case 2:
                if(clue_diary == 0) {
                    printf("피해자의 일기장을 발견했다.\n");
                    clue_diary = 1;
                    count++;
                } else {
                    printf("이미 조사한 항목입니다.\n");
                }
                break;
            case 3:
                if(clue_medicine == 0) {
                    printf("한지우가 숨긴 약품을 발견했다.\n");
                    clue_medicine = 1;
                    count++;
                } else {
                    printf("이미 조사한 항목입니다.\n");
                }
                break;
            default:
                printf("잘못된 입력입니다.\n");
                break;
        }
        printf("\n");
    }
}

void analyze() {
    printf("단서들을 종합해 범인을 추리할 시간이다.\n");
    printf("누가 범인이라고 생각하는가?\n");
    printf("1. 한지우\n");
    printf("2. 박서진\n");
    printf("3. 최윤호\n");
    printf("선택: ");
}

void ending() {
    int guess;
    scanf("%d", &guess);

    printf("\n=== 결과 ===\n");
    if(guess == 1) {  // 한지우가 범인일 때
        if(clue_phone && clue_prescription && clue_medicine) {
            printf("당신의 추리가 맞았다! 한지우가 범인이다.\n");
            printf("그는 자신의 과거를 숨기려 범행을 저질렀다.\n");
            printf("게임을 성공적으로 마쳤다!\n");
        } else {
            printf("증거가 부족하다! 한지우를 확신하기 어렵다.\n");
            printf("범인은 도망쳤다... 게임 실패!\n");
        }
    } else if(guess == 2) {
        printf("박서진은 범인이 아니다.\n");
        printf("잘못된 선택으로 게임 실패!\n");
    } else if(guess == 3) {
        printf("최윤호는 이미 죽은 상태이다.\n");
        printf("잘못된 선택으로 게임 실패!\n");
    } else {
        printf("잘못된 입력입니다.\n");
    }
} 
