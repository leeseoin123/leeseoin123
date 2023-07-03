GlowScript 2.7 VPython
##45도경우 (공기저항있음)
##온도 25도 라고 가정
floor = box(length = 60, height = 0.5, width = 4, color = color.yellow)

ball = sphere(pos = vector(-28, 1, 0), radius = 1, color = color.red, make_trail = True)
##공기저항없는공
ball2 = sphere(pos = vector(-28, 1, 0), radius = 1, color = color.green, make_trail = True)
##공기저항있는공
dt = 0.01
v = 10
m = 10
r = 1
cnt1 = 1
cnt2 = 1
print('속도를 설정해 주세요. 초기 속도는 10 입니다.')
while(True):
    ev = scene.waitfor('click keydown')
    if ev.event == 'click':
        print('속도 설정 완료, 질량을 설정해 주세요.')
        break
    if ev.event == 'keydown':
        v = v + 5
        print('현재 속도 : ' + v)

print('초기 질량은 10kg 입니다.')
while(True):
    ev = scene.waitfor('click keydown')
    if ev.event == 'click':
        print('질량 설정 완료, 시작하려면 클릭하세요!')
        break
    if ev.event == 'keydown':
        m = m + 10
        print('현재 질량 : ' + m + 'kg')
scene.waitfor('click keydown')

ball.velocity = vector(((sqrt(2))/2) * v, ((sqrt(2))/2) * v, 0)
ball2.velocity = vector(((sqrt(2))/2) * v, ((sqrt(2))/2) * v, 0)

label(pos=ball.pos, text='Start!',font='sans',  height=12)
print('공 초기 위치: ' + '0')
while(True):
    rate(500)
    ball2.pos = ball2.pos + ball2.velocity * dt
    ball.pos = ball.pos + ball.velocity * dt        
    if ball.pos.y <= 0.75:
        ball.velocity.y = -ball.velocity.y
        newpos1 = ball.pos.x + 28
        print ('공기저항 없는 공 ' + cnt1 + '번째 위치: ' + newpos1)
        label(pos=ball.pos, text=newpos1,font='sans', height=12)
        cnt1 = cnt1 + 1
    else:
        ball.velocity.y = ball.velocity.y + -9.8 * dt
    
    if ball2.pos.y <= 0.75:
        ball2.velocity.y = -ball2.velocity.y
        newpos2 = ball2.pos.x + 28
        print ('공기저항 있는 공 ' + cnt2 + '번째 위치: ' + float(newpos2))
        label(pos=ball2.pos, text=newpos2,font='sans', height=12)
        cnt2 = cnt2 + 1
    else:
        if ball2.velocity.y > 0:
            ally = (-3.496 * ball2.velocity.y * ball2.velocity.y) / m
        else:
            ally = (3.496 * ball2.velocity.y * ball2.velocity.y) / m
        allx = (3.496 * ball2.velocity.x * ball2.velocity.x) / m
        ball2.velocity.y = ball2.velocity.y + -1 * (9.8 - ally) * dt
        ball2.velocity.x = ball2.velocity.x + - allx * dt
        
    if cnt1 == 2:
        ball.pos = vector(newpos1-28, 1, 0)
        ball.velocity = vector(0, 0, 0)
    if cnt2 == 2:
        ball2.pos = vector(newpos2-28, 1, 0)
        ball2.velocity = vector(0, 0, 0)

