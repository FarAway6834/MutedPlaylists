# 파일 업로드 시스템

커스텀 애러 객체는,
영어를 못읽는 사람들을 위해,
[Error명]_ErrorCode[16진수 리트체]로 명명함.
사실 개인용이라서 코드짜기 귀찮은거지만

base_playlist 클래스의 객체
 - 베이스는 url 리스트임
 - addf(file) 메서드로, URL.createObjectURL(file)해서 append시킴
 - delf(file) 메서드로, URL.revokeObjectURL(file)해서 삭제시킴
 - file_curser 어트리뷰트가 존재함 (숫자임)
 - turn_table_setting_core(turn_table) 메서드는, 모듈화 용도로 따로 함수화한 것으로 turn_table.src = this[file_curser]로, 파일을 설정해줌
 - put_it_on_the_turn_table(turn_table) 메서드를 쓰면, 내부에 숨겨진 curser_data_regularize_preprocessing() 메서드를 호출한 후, turn_table_setting_core(turn_table) 메서드를 호출함
 - curser_data_regularize_preprocessing()메서드는 file_curser = file_curser % this.length 만 스행함.
 - 따로 제한하지 않지만, 원칙적으로 url만 담겨야함, 실사용 용도 클래스가 아님 (타입 안전하지 않음)

pre_playlist 클래스(base_playlist를 상속)의 객체
 - url말고도 pre_playlist계열 객체 또한, 플리(플래이리스트)에 포함될수 있음
 - put_it_on_the(turn_table) 메서드를 사용하면, 내부에 숨겨진 curser_data_regularize_preprocessing() 메서드를 호출한 후, 커서가 가르키는 위치 (this[file_curser]가 가르키는거)가 url이면 turn_table_setting_core(turn_table)을 호출하고, url이 아닌 pre_playlist계열 객체면, this[file_curser].put_it_on_the(turn_table)로 해당 플리에서 재생함.
 - 따로 제한하진 않지만, 원칙적으로 url이나 pre_playlist계열 객체만 포함해야함, 따라서, pre_playlist계열 객체인지 url인지 판단할때, url이 아닌데 pre_playlist계열 객체도 아니라면, PlaylistElementException_ErrorCode09EE(Playlist Elemebt Exception이므로, PEE를 9EE로)을 발생시킴.
 - 인코드 문서수준에서, 타입세이프하게 상속한다음에 사용할것을 권장하므로, pre_playlist를 playlist로 바꾸기 전에 커스텀할 자유를 주지만, 대신에 프로그래머가 처신을 잘해야한다. (C언어가 그렇듯, 자유를 주지만 처신을 잘해야한다.)

---

[링크 돌아가는거 있음좋겠는데 귀찮](https://github.com/FarAway6834/MutedPlaylists/tree/main)