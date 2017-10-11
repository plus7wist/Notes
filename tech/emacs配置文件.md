---
title: #emacs 配置文件
---

[2016/05/20]

```lisp?linenums
;; 把 .emacs.d 目錄加入到 load-path
;; 這樣的話本來需要放到 /usr/share/emacs/site-lisp/ 的東西
;; 就只需要放到 .emacs.d 裏面
(add-to-list 'load-path "~/.emacs.d/")




;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;                                                                        ;;
                    ; 軟件界面
;;                                                                        ;;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;

;; 去掉歡迎界面
(setq inhibit-startup-message t)

;; 在标题栏提示文件名字
(setq frame-title-format "gu_castle@ %b")

;; 去掉工具栏
(tool-bar-mode nil)

;;去掉菜单栏
(menu-bar-mode nil)

;; 顯示行號
;; 1) linum.el 放入 .emacs.d
(require 'linum) ;; 引用包
(global-linum-mode) ;; 在全局使用顯示行號的模式

;; 去掉滚动栏
(scroll-bar-mode nil)

;; 顯示時間
(display-time-mode 1)
(setq display-time-24hr-format t)
(setq display-time-day-and-date t)

;; 启动窗口大小
(setq default-frame-alist
      '((height . 37) (width . 85)
    (menu-bar-lines . 20) (tool-bar-lines . 0)))




;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;                                                                        ;;
                    ; 編輯界面
;;                                                                        ;;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;

;; 選擇高亮配色
;; 1) color-theme.el 和 theme 文件夹放入 .emacs.d
;; 2) 打開 Emacs，按 'M-x color-theme-select'，選擇配色，按回車查看效果
;; 3) 選好你中意的效果，然後按 d 出現配色的描述信息，以 matrix 配色爲例子：
;;    color-theme-matrix is an interactive Lisp function in
;;    `color-theme-library.el'.
;;    (color-theme-matrix)
;;    Color theme by walterh@rocketmail.com, created 2003-10-16.
;; 4) 進入 .emacs 寫入 (color-theme-matrix)。
(require 'color-theme)
(color-theme-initialize)
(setq color-theme-is-global t)
;;(color-theme-xp)
;;(color-theme-high-contrast)
;;(color-theme-classic)
;;(color-theme-jb-simple)
;;(color-theme-arjen)
(color-theme-matrix)

;; 显示括号匹配
(show-paren-mode t)
(setq show-paren-style 'parentheses)

;; 回车缩进
(global-set-key "\C-m" 'newline-and-indent)
(global-set-key (kbd "C-<return>") 'newline)

;; 設置字體
;; 1) emacs->options->Set Default Font 選擇字體
;; 2) "M-x describe-font" & RET
;; 3) 將第一行冒號後的部分抄到下面的引號裏面

;;(set-default-font
;; " -unknown-Ubuntu Mono-normal-normal-normal-*-15-*-*-*-m-0-iso10646-1")
;; Ubuntu Mono

;;(set-default-font
;; " -outline-DejaVu Sans Mono-normal-normal-normal-mono-16-*-*-*-c-*-iso8859-2")
;; DejaVu Sans Mono

;;(set-default-font
;;"-outline-Lucida Console-normal-normal-normal-mono-16-*-*-*-c-*-iso10646-1")
;; Lucida Console

(set-default-font
 "-outline-Andale Mono-normal-normal-normal-mono-16-*-*-*-c-*-iso10646-1")
;; Andale mono

;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;                                                                        ;;
                    ; 其他功能
;;                                                                        ;;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;

;;使用 y or n 提問
;;(fset 'yes-or-no-p' 'y-or-n-p')

;; 支持emacs和外部程序的粘贴
(setq x-select-enable-clipboard t)

;; 不產生備份文件
(setq-default make-backup-files nil)

;; 不自動去掉行尾空格
(setq delete-trailing-whitespace nil)

;; 設置默認查找文件的目錄
(setq default-directory "d:/Documents/")

;; 移動到第 n 行：M-g n
(global-set-key [(meta g)] 'goto-line)

;; 插入當前時間
(defun insert-curtime()
  "insert current time"
  (interactive "*")
  (insert (current-time-string)))

;; Eshell 清屏
(defun eshell/cls()  
  "to clear the eshell buffer."  
  (interactive)  
  (let ((inhibit-read-only t))
    (erase-buffer)))

;; hs-minor-mode 按鍵綁定
;; 如果要使用這個鍵，先運行 M-x hs-minor-mode
(global-set-key (kbd "M-,") 'hs-toggle-hiding)
```