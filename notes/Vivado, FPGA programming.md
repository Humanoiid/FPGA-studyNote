# Vivado, FPGA programming

## Reference for vivado FPGA programming

link: [https://m.blog.naver.com/rlaghlfh/221148822517](https://m.blog.naver.com/rlaghlfh/221148822517)

## VHDL programming example

link: [https://m.blog.naver.com/rlaghlfh/221148822517](https://m.blog.naver.com/rlaghlfh/221148822517)

## Verilog study

link: [https://m.blog.naver.com/PostView.nhn?blogId=kijul&logNo=110183456902&proxyReferer=https:%2F%2Fwww.google.com%2F](https://m.blog.naver.com/PostView.nhn?blogId=kijul&logNo=110183456902&proxyReferer=https:%2F%2Fwww.google.com%2F)

# Vivado - XDC (Design Constraint)

link: [https://www.xilinx.com/support/documentlinkation/sw_manuals/xilinx2018_1/ug903-vivado-using-constraints.pdf](https://www.xilinx.com/support/documentlinkation/sw_manuals/xilinx2018_1/ug903-vivado-using-constraints.pdf)

1. XDC (Xilinx Design Constraints) file: 
    1. constraints file for xilinx. (not for general support (ex. UCF: User Constriants file))
    2. 구성: industry standard(synopsys design constriants(SDC v1.9) + Xilinx proprietary physical constrainst)
2. 기타설명링크: [http://wiki.vctec.co.kr/devboard/fpga/spartan-3a-fpga-gaebalbodeu--elbert/synthesis](http://wiki.vctec.co.kr/devboard/fpga/spartan-3a-fpga-gaebalbodeu--elbert/synthesis)
    1. Constraint 파일을 정의함으로서, logic과 물리적 핀의 연결을 위한 정보를 사전에 정의함.
    2. 모든 IO 정보를 기록함
- 요약: General XDC 파일 기반으로 필요에 따라 사용할 I/O 포트 활성화 해줌
    - 원본 XDC 파일 기반으로 필요에 따라 I/O 핀의 주석처리 및 port name만 관리하면 됨
    - 최하단 추가 내용은 다음과 같으며, 필요에 따라 global constraints를 수정 가능
        - BITSTREAM.GENERAL.COMPRESS TRUE (bitstream의 크기 줄임)
        - BITSTREAM.CONFIG.CONFIGRATE 33(Master mode에서 내부 oscillator 기반 CCLK ratio)
        - CONFIG_MODE SPIx4: SPI 통신 4bit width 로 설정. 기타 레퍼런스 참고시 대략 메모리에 올리는 통신방법 비슷한 것으로 보임

# Vivao FPGA design / Project

참고 링크: [https://m.blog.naver.com/rlaghlfh/221148822517](https://m.blog.naver.com/rlaghlfh/221148822517)

디자인 순서

1. 계획, 예산 정립 후
2. 코드 작성 (VHDL, Verilog)
3. RTL(register-transfer level) 시뮬레이션 수행
    - clock에 따라 회로를 동기화, 데이터를 읽고 쓸 수 있음. 변수처럼 선언하여 사용
4. synthesis(합성) → netlist 만듬 (실제 디지털 회로로 구성)
5. implementation(Translate, Map, Place&Route) 실제 디지털회로 배치 배선
6. timing simulation
7. generate bit file → FPGA에 최종적으로 업로드 함

## Project 생성 및 관리

일반적인 vivado 프로젝트 만들기

1. RTL 프로젝트 생성
2. 필요한 소스코드 추가

⇒ 일반적인 프로젝트 기준

1. Library: 보통 IEEE 라이브러리 가져와서 사용
2. Entity: 해당 모듈이 사용할 I/O 포트를 선언
3. Architecture: Entity가 어떤 기능을 할 것인지 정의해줌 (코드의 대부분)
    - 회로 동작 및 내부 연결상태 설정

## Programming

1. Simulation > Run Simulation
    1. by changing switch value, we can control the situation when we use switch.
2. FPGA 연결 후 
    1. Synthesis 진행: CPU 논리프로세서 수 만큼 작업 돌릴 수 있음, 다소 시간 소요
    2. Run implementation: 위와 유사함, 다소 시간 소요
    3. generation bit sitmulation: FPGA에 업로드 할 프로그램으로 만들어줌, 다소 시간 소요
        - 헷갈리면 이것 바로 실행하여 한번에 진행하면 될 것
        - 에러 발생시, 레퍼런스 참고하여 수정하기
        - 정상적으로 bit 파일 생성시, Open Hardware Manager > Open Target > Program Device 수행하면, 작동 됨
            - 처음 이용시 아래 이름의 memory를 configure 해주어야 함 (nexys-A7-100T 기준)
                - datasheet 기준 3.2 Quad-SPI Flash (12pg)에 해당 모델 명 있음 (Link: [https://reference.digilentinc.com/_media/reference/programmable-logic/nexys-a7/nexys-a7_rm.pdf](https://reference.digilentinc.com/_media/reference/programmable-logic/nexys-a7/nexys-a7_rm.pdf))
                - 각 보드별 지원 메모리 데이터 시트도 있음
                Link: [https://www.xilinx.com/support/documentation/sw_manuals/xilinx2019_2/ug908-vivado-programming-debugging.pdf](https://www.xilinx.com/support/documentation/sw_manuals/xilinx2019_2/ug908-vivado-programming-debugging.pdf)

                
            - 해당 memory 내에 프로그래밍 해주어야 실질적으로 메모리에 값이 저장됨
            - 안전하게 하드웨어 해제한 뒤, Mode 변경하기 (JTAG → QSPI: 내부 플래시에 프로그래밍된 것 실행)
        - + 실제로 Flash programming 이 안되면, Xilinx 자체에서 에러가 나타나고, 정확한 파트 번호를 알려주는것으로 보임
