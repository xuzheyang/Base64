# Base64  

## 原理  

3 * 8 = 4 * 6
内存1个字节占8位
转前： s 1 3
先转成ascii：对应 115 49 51
2进制： 01110011 00110001 00110011
6个一组（4组） 011100110011000100110011
然后才有后面的 011100 110011 000100 110011
然后计算机是8位8位的存数 6不够，自动就补两个高位0了
所有有了 高位补0
科学计算器输入 00011100 00110011 00000100 00110011
得到 28 51 4 51
查对下照表 c z E z


## 例子  

~~~
#include "Base64.h"

static std::string encode (const std::string& encode) {
	int inputLen = encode.length();

	char *input =  (char *)malloc(inputLen);

	strcpy(input, encode.c_str());

	int encodedLen = base64_enc_len(inputLen);
	char *encoded = (char *)malloc(encodedLen);

	base64_encode(encoded, encode.c_str(), inputLen); 
	std::string ret = encoded;

	free(input);
	free(encoded);
	
	return ret;
}

static std::string decode (const std::string& decode) {
	int inputLen = (int) decode.length();

	char *input =  (char *)malloc(inputLen);

	strcpy(input, decode.c_str());

	int decodedLen = base64_dec_len(input, inputLen);
	char *decoded = (char *)malloc(decodedLen);

	base64_decode(decoded, input, inputLen);
	std::string ret = decoded;

	free(input);
	free(decoded);

	return ret;
}

int main(int argc, char *argv[]) {
	std::string str = "hello world!"
	std::cout << "str: " << str << std::endl;

	str = encode(str);
	std::cout << "encode: " << str << std::endl;

	str = decode(str);
	std::cout << "decode: " << str << std::endl;
}

~~~



