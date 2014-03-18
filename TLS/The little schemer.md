---
layout: post
title:  The Little Schemer
date:   2014-03-20
---
```scheme
;;����һ�������Ƿ���ԭ��
;;�Ӻ������忴����scheme�У�ֻҪ���ǵ�ԺͷǿյĶ�����ԭ��
;;scheme��ԭ���ǲ����ٷֵ���С��λ�������Ȼ���ǣ��б�Ҳ����
;;һ�����б�'()��Ȼ�����ٷֳɸ�С����ɲ��֣����ǿ��б���Ȼ
;;����ԭ��
;;ò�Ʋ������е�schemeʵ���ж���atom?�����������ڱ���һ��ͷ
;;��Ҫ����߶�������һ������
(define atom?
  (lambda (x)
    (and (not (pair? x)) (not (null? x)))))

;;�����ߵĶ����У�lat������һ���б�
;;�б��е�ÿһ��Ԫ�ض��ǵ�����ԭ�ӣ�û��Ƕ�������б�
;;���б�Ҳ����lat                       (p19)
(define lat?
  (lambda (l)
    (cond
     ((null? l) #t)
     ((atom? (car l)) (lat? (cdr l)))
     (else #f))))

;;���Զ���a�Ƿ����б�lat�ĳ�Ա֮һ      (p22)
;;���ں�������ľ��ޣ�a������һ�����б�
;;�����õ�����Ĵ𰸣�������ݸ�������
;;����a��һ�����б�������ȷ�Ľ��Ӧ����#t
(define member?
  (lambda (a lat)
    (cond
     ((null? lat) #f)
     (else (or (eq? (car lat) a)
               (member? a (cdr lat)))))))

;;���б�lat�в��Ҷ���a������ҵ���ɾ��
;;������б�lat�к��в�ֹһ��a����ֻɾ���ҵ��ĵ�һ����p41��
(define rember
  (lambda (a lat)
    (cond
     ((null? lat) '())
     ((eq? (car lat) a) (cdr lat))
     (else (cons (car lat)
                 (rember a (cdr lat)))))))

;;�б�l�����������Ľṹ��
;;'((a b) (c d) (e f))
;;firsts���������Ա�б���ȡ����һ��Ԫ��
;;���һ���µ��б�             (p44)
;;'(a c e)
(define firsts
  (lambda (l)
    (cond
     ((null? l) '())
     (else (cons (car (car l)) (firsts (cdr l)))))))

;;���б�lat��Ѱ��old���ҵ���new���뵽old��
;;�ұߣ����һ�����б�                (p50)
(define insertR
  (lambda (new old lat)
    (cond
     ((null? lat) '())
     ((eq? old (car lat)) (cons old (cons new (cdr lat))))
     (else
      (cons (car lat) (insertR new old (cdr lat)))))))

;;����һ���������ƣ���ͬ����new���뵽old�����  (p51)
(define insertL
  (lambda (new old lat)
    (cond
     ((null? lat) '())
     ((eq? old (car lat)) (cons new lat))
     (else
      (cons (car lat) (insertL new old (cdr lat)))))))

;;���б��в���old���ҵ�����new�滻�����������б�  (p51)
(define subst
  (lambda (new old lat)
    (cond
     ((null? lat) '())
     ((eq? (car lat) old) (cons new (cdr lat)))
     (else
      (cons (car lat) (subst new old (cdr lat)))))))

;;����һ���������ƣ�����oldֵ��������o1��o2
;;�������б����ҵ���һ��oldֵ��������new����
;;�滻                                        (p52)
(define subst2
  (lambda (new o1 o2 lat)
    (cond
     ((null? lat) '())
     ((eq? (car lat) o1) (cons new (cdr lat)))
     ((eq? (car lat) o2) (cons new (cdr lat)))
     (else (cons (car lat)
                 (subst2 new o1 o2 (cdr lat)))))))

;;rember�������ƣ����б���ɾ��һ����Ա
;;��ͬ���ǣ�remberֻɾ�����ҵ��ĵ�һ��
;;��Ա����������ɾ��������a��ͬ�ĳ�Ա      (p53)
(define multirember
  (lambda (a lat)
    (cond
     ((null? lat) '())
     ((eq? a (car lat)) (multirember a (cdr lat)))
     (else
      (cons (car lat) (multirember a (cdr lat)))))))

;;;(p56)
(define multiinsertR
  (lambda (new old lat)
    (cond
     ((null? lat) '())
     ((eq? (car lat) old)
      (cons old (cons new
                      (multiinsertR new old (cdr lat)))))
     (else
      (cons (car lat) (multiinsertR new old (cdr lat)))))))

;;���ز������(p57)
(define multiinsertL
  (lambda (new old lat)
    (cond
     ((null? lat) '())
     ((eq? (car lat) old)
      (cons new (cons old (multiinsertL new old (cdr lat)))))
     (else
      (cons (car lat)
            (multiinsertL new old (cdr lat)))))))

;;�����滻(p57)
(define multisubst
  (lambda (new old lat)
    (cond
     ((null? lat) (quote ()))
     ((eq? (car lat) old)
      (cons new (multisubst new old (cdr lat))))
     (else
      (cons (car lat)
            (multisubst new old (cdr lat)))))))


(define add1
  (lambda (n)
    (+ n 1)))

(define sub1
  (lambda (n)
    (- n 1)))

;;���¶��塰+����,Ϊ����ϵͳ���ú�����ͻ(p60)
;;��������Ϊo+
(define o+
  (lambda (m n)
    (cond
     ((zero? m) n)
     (else (add1 (o+ n (sub1 m)))))))

;;���¶������(p61)
(define o-
  (lambda (m n)
    (cond
     ((zero? n) m)
     (else (sub1 (o- m (sub1 n)))))))

;;�����������ֹ��ɵ��б���ӣ������ܺͣ�p64��
(define addtup
  (lambda (tup)
    (cond
     ((null? tup) 0)
     (else
      (o+ (car tup) (addtup (cdr tup)))))))

;;���¶���˷���ͨ���ӷ���ʵ�ֳ˷�(p65)
(define x
  (lambda (n m)
    (cond
     ((zero? m) 0)
     (else
      (o+ n (x n (sub1 m)))))))

;;�����������б���ӣ�����һ�����б�
;;(tup++ '(1 2 3) '(4 5 6))
;;=>(5 7 9)
;;�˺����и����ޣ���Ϊ�����������б�Ԫ������������ͬ(p69)
(define tup++
  (lambda (tup1 tup2)
    (cond
     ((and (null? tup1) (null? tup2))
      '())
     (else
      (cons (o+ (car tup1) (car tup2))
            (tup+ (cdr tup1) (cdr tup2)))))))

;;����һ���������ƣ��������Խ����������Ȳ�ͬ���б�������(p71)
(define tup+
  (lambda (tup1 tup2)
    (cond
     ((null? tup1) tup2)
     ((null? tup2) tup1)
     (else
      (cons (o+ (car tup1) (car tup2))
            (tup++ (cdr tup1) (cdr tup2)))))))

;;���¶�����ں�
(define >>
  (lambda (n m)
    (cond
     ((zero? n) #f)
     ((zero? m) #t)
     (else (>> (sub1 n) (sub1 m))))))
     
```