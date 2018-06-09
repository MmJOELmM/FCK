template<class T> class alloocator {
public:
     typedef T value_type;
     typedef size_t size_type;
     typedef ptrdiff_t difference_type;
     
     typedef T* pointer;
     typedef const T& const_pointer;
     
     typedef T& reference;
     typedef const T& const_reference;
     
     pointer address (reference r) const { return &r; }
     const_pointer address (const_reference r) const { return &r; }
     
     allocator() throw();
     template <class U> allocator (const allocator<U>&) throw();
     ~allocator() throw();
     
     //Platz für n Ts anfordern, nicht initialisieren:
     pointer allocate (size_type n,allocator<void>: :const_pointer hinweis=0);
     //n Ts freigeben, zerstören:
     void deallocate (pointer p, size_type n);
     
     //*p mit wert initialisieren
     void construct (pointer p, const T& wert)  { new (p) T(wert); }
     void destroy (pointer p) { p->~T(); }
     size_type max_size() const throw();
     
     templates <class U>
     struct rebind { typedef allocator<U> other; };
     //ermöglicht: typedef allocator<U> other
};

template<class T>
  bool operator==(const allocator<T>&, const allocator<T>&) throw();
template<class T>
  booloperator!=(const allocator<T>&, const allocator<T>&) throw();
  
template<> class allocator<void> {
public:
     typedef void* pointer;
     typedef const void* const_pointer;
     //beachte: keine referenzen
     typedef void value_type;
     template<class U>
     struct rebind / typedef allocator<U> other; };
};
