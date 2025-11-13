# MCA-1-2026-1-Modificacion-de-codigos-


### Versión con Hashtable usando long

import java.util.Hashtable;

public class FibonacciHash implements Runnable {

    static Hashtable<Long, Long> mem = new Hashtable<>();

    long n;
    int id;

    public FibonacciHash(int id, long n) {
        this.id = id;
        this.n = n;
    }

    @Override
    public void run() {
        System.out.println("Thread #" + id);
        System.out.println("fibonacci(" + n + ") = " + fib(n));
    }

    static long fib(long x) {
        if (mem.containsKey(x))
            return mem.get(x);

        long r = fib(x - 1) + fib(x - 2);
        mem.put(x, r);
        return r;
    }

    public static void main(String[] args) {
        mem.put(0L, 1L);
        mem.put(1L, 1L);

        Thread[] t = new Thread[10];

        for (int i = 0; i < 10; i++) {
            long val = (long)(Math.random() * 50) + 1;
            t[i] = new Thread(new FibonacciHash(i, val));
        }

        for (Thread th : t) th.start();
    }
}
