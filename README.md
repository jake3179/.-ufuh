# jake차소웨과제
#include <iostream>
#include <fstream>
#include <regex>
#include <string>

int main() {
    std::string filename, pattern;

    // 사용자로부터 파일 이름과 검색할 패턴을 입력받음
    std::cout << "텍스트 파일 이름을 입력하세요: ";
    std::cin >> filename;
    std::cout << "검색할 패턴(정규식)을 입력하세요: ";
    std::cin >> pattern;

    // 파일 열기
    std::ifstream file(filename);
    if (!file.is_open()) {
        std::cerr << "파일을 열 수 없습니다: " << filename << std::endl;
        return 1;
    }

    // 정규식 객체 생성
    std::regex regex_pattern(pattern);
    std::string line;
    int line_number = 0;

    // 파일의 각 줄을 읽어 정규식 패턴과 매칭되는지 확인
    while (std::getline(file, line)) {
        line_number++;
        std::smatch matches;
        if (std::regex_search(line, matches, regex_pattern)) {
            std::cout << "라인 " << line_number << ": " << line << std::endl;
        }
    }

    file.close();
    return 0;
}
