**BGP (Border Gateway Protocol) ek standard routing protocol hai, jo Internet par data packets ko unki manzil tak pahunchane ka kaam karta hai. Socho, BGP Internet ke "GPS" jaisa hai jo data ko sabse chote aur sabse efficient raste se bhejta hai.

---

## BGP Kaise Kaam Karta Hai?

BGP ka mukhya kaam yeh pata lagana hai ki Internet par maujood laakhon networks (jinhe **Autonomous Systems - AS** kehte hain) ke beech data ko kaise bhej na hai. Har AS ek bade organization ya service provider ka network hota hai, jaise Google, Amazon ya Airtel ka network.

BGP in Autonomous Systems ke beech ek "trust" banata hai, jisse ve ek doosre ke network routes ke baare mein jaankari share karte hain.

- **Path Vector Protocol:** BGP ek **Path Vector Protocol** hai. Iska matlab hai ki jab bhi koi AS kisi doosre AS ko koi route batata hai, to woh poora rasta (path) bhi batata hai ki data kin-kin ASs se hokar guzra hai. Isse BGP ko yeh samajhne mein madad milti hai ki kaunsa rasta sabse chota ya behtar hai, aur networking loops se bhi bachta hai.
    
- **Routing Decisions:** BGP sirf ek rasta nahi chun ta, balki kayi factors par consider karta hai, jaise ki:
    
    - Raste ki lambaai (number of ASs)
    - Network administrator ki preferences
    - Network ka performance

In sab factors ke adhaar par, BGP best route chun ta hai aur usko apne routing table mein store kar leta hai.

Simple shabdo mein, BGP ek router ko doosre router se milata hai aur unhe Internet ka sabse behtar aur sabse chota rasta batata hai, jisse aapki website ek click mein load ho jaati hai.**