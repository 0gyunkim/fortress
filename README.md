# 자바스크립트를 이용한 슈팅게임
### 사용법
* 공격이 가능한 캐릭터를 선택 후 타겟을 선택한다
* 게임이 시작되면 키보드 W,A,S,D와 방향키 위, 아래, 스페이스바를 이용하여 공격자의 위치 및 대포의 각도를 조절한다
* 타겟은 미사일을 발사하면 위치가 변경된다
* 미사일을 총 10발이 주어지고 6발 이상 맞추면 승리한다
### 흐름도
![흐름도](https://github.com/0gyunkim/fortress/assets/153244950/2a949b28-3b2c-4b81-b75f-3ba66554b44c)
### 시연 영상
https://github.com/0gyunkim/fortress/assets/153244950/b7627384-9281-4dbb-86ac-5fac40882910
### 기술 스택
**▷ 이벤트 리스너 활용** <br>
자바스크립트 문법에 EventListener를 사용하여 탱크와 대포를 이동할 수 있도록 구현
```
    document.addEventListener("keydown", keydownHandler, false);
    document.addEventListener("keyup", keyupHandler, false);
```
```
    const keydownHandler = event => {
        if (event.keyCode === 65) {
            tankLeftPressed = true;
        } else if (event.keyCode === 68) {
            tankRightPressed = true;
        } else if (event.keyCode === 87) {
            tankUpPressed = true;
        } else if (event.keyCode === 83) {
            tankDownPressed = true;
        } else if (event.keyCode === 38 && cannonAngle <= 1.87) {
            cannonAngle = cannonAngle + cannonAngleDIF
        } else if (event.keyCode === 40 && cannonAngle >= 0.78) {
            cannonAngle = cannonAngle - cannonAngleDIF;
        } else if (event.keyCode === 32 && !isFired) {
            isCharging = true;
        }
    }
    const keyupHandler = event => {
        if (event.keyCode === 65) {
            tankLeftPressed = false;
        } else if (event.keyCode === 68) {
            tankRightPressed = false;
        } else if (event.keyCode === 87) {
            tankUpPressed = false;
        } else if (event.keyCode === 83) {
            tankDownPressed = false;
        } else if (event.keyCode === 32 && !isFired) {
            isCharging = false;
            isFired = true;
            missilePower = powerGauge * 1.45;
            if (missilePower < 6) {
                missileDx = missilePower * 0.7 * Math.cos(cannonAngle);
                missileDy = missilePower * 0.7 * Math.sin(cannonAngle);

            } else if (missilePower > 6 && missilePower < 8.5) {
                missileDx = missilePower * Math.cos(cannonAngle);
                missileDy = missilePower * Math.sin(cannonAngle);
            } else {
                missileDx = missilePower * 1.3 * Math.cos(cannonAngle);
                missileDy = missilePower * 1.3 * Math.sin(cannonAngle);
            }
            missileDy = missilePower * Math.sin(cannonAngle);
            powerGauge = Math.PI;
            missilecnt++;
        }

    }
```


