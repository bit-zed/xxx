import string
import re

table ='ACKMYBXWTHFIVDZEPackmybxwthfivdzenlqorjugspNLQORJUGS'+string.digits + '+/'

def encode(origin_bytes):

    getdBytes = ['{:0>8}'.format(str(bin(b)).replace('0b', '')) for b in origin_bytes]
    resp = ''
    nums = len(getdBytes) // 3
    remain = len(getdBytes) % 3

    integral_part = getdBytes[0:3 * nums]
    while integral_part:
        tmp_unit = ''.join(integral_part[0:3])
        tmp_unit = [int(tmp_unit[x: x + 6], 2) for x in [0, 6, 12, 18]]
        resp += ''.join([table[i] for i in tmp_unit])
        integral_part = integral_part[3:]
    if remain:
        remain_part = ''.join(getdBytes[3 * nums:]) + (3 - remain) * '0' * 8
        tmp_unit = [int(remain_part[x: x + 6], 2) for x in [0, 6, 12, 18]][:remain + 1]
        resp += ''.join([table[i] for i in tmp_unit]) + (3 - remain) * '='
    return resp


if __name__ == '__main__':
    s = 'flag{***************************}'.encode()
    encflag = encode(s)
    print('encflag is：', encflag)
    #encflag is： tjUnt3Q0hXrSxSBSx2BztbBSdy9lwxDrDqazijyJfXBqty90wbHLtx0=
