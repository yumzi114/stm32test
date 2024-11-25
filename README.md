# stm32test

# 간단한 수동설정시
## config.toml 설정 (칩셋에 따라) probe 로 빌드
 
https://blog.naver.com/sheld2/223083276587?trackingCode=rss

[target.'cfg(all(target_arch = "arm", target_os = "none"))']
runner = "probe-rs run --chip STM32F401RETx"
[target.thumbv7em-none-eabihf]
rustflags = [
    "-C", "link-arg=-Tlink.x",
    # "-C", "link-arg=-Tdefmt.x",
]
[build]
target = "thumbv7em-none-eabihf"

## memory.x파일 : 링커 스크립트
보드 사양확인 후 설정 CUBE MX 에서 데이터시트

MEMORY
{
    FLASH (rx) : ORIGIN = 0x08000000, LENGTH = 512K
    RAM (rxw)  : ORIGIN = 0x20000000, LENGTH = 96K
}
_stack_start = ORIGIN(RAM) + LENGTH(RAM);

## 러스트 공식문서(임베디드 STM예시) 정리잘되어있는
https://docs.rust-embedded.org/book/intro/install.html