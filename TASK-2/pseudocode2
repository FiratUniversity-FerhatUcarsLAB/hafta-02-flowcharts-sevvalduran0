BEGIN Online_Shopping_Session

    DISPLAY "Ürün Kataloğu"
    
    WHILE User_is_Browsing DO
        product = SELECT_PRODUCT()
        action = PROMPT("Ürünü sepete eklemek için 'add', çıkarmak için 'remove', bitirmek için 'done'")
        
        IF action == 'add' THEN
            quantity = PROMPT("Kaç adet?")
            ADD_TO_CART(product, quantity)
            DISPLAY_CART()
        
        ELSE IF action == 'remove' THEN
            REMOVE_FROM_CART(product)
            DISPLAY_CART()
        
        ELSE IF action == 'done' THEN
            BREAK
        ENDIF
    END WHILE

    IF IS_CART_EMPTY() THEN
        DISPLAY "Sepetiniz boş. Çıkılıyor..."
        TERMINATE_SESSION()
        RETURN
    ENDIF

    // Kullanıcı Girişi veya Kayıt
    IF NOT IS_USER_LOGGED_IN() THEN
        option = PROMPT("Giriş için 1, Yeni kayıt için 2")
        
        IF option == 1 THEN
            WHILE NOT LOGIN_SUCCESSFUL() DO
                PROMPT_FOR_LOGIN()
            END WHILE
        ELSE IF option == 2 THEN
            REGISTER_NEW_USER()
            LOGIN_USER()
        ENDIF
    ENDIF

    // Adres ve Kargo
    IF NOT HAS_SAVED_ADDRESS() THEN
        PROMPT_AND_SAVE_ADDRESS()
    ENDIF
    DISPLAY_SHIPPING_OPTIONS()
    shipping_method = SELECT_SHIPPING_METHOD()

    // Ödeme Yöntemi Seçimi
    DISPLAY_PAYMENT_OPTIONS()
    payment_method = SELECT_PAYMENT_METHOD()

    IF payment_method == "CreditCard" THEN
        card_info = PROMPT_CARD_DETAILS()
        IF NOT VALIDATE_CARD(card_info) THEN
            DISPLAY "Kart bilgileri geçersiz"
            TERMINATE_SESSION()
            RETURN
        ENDIF
    ELSE IF payment_method == "EFT" THEN
        DISPLAY_BANK_ACCOUNT_DETAILS()
        WAIT_FOR_TRANSFER_CONFIRMATION()
    ELSE IF payment_method == "PayPal" THEN
        REDIRECT_TO_PAYPAL()
        IF NOT PAYPAL_PAYMENT_SUCCESSFUL() THEN
            DISPLAY "PayPal ödemesi başarısız"
            TERMINATE_SESSION()
            RETURN
        ENDIF
    ENDIF

    // Ödeme İşlemi
    IF PROCESS_PAYMENT(payment_method) THEN
        ORDER_ID = CREATE_ORDER()
        SEND_ORDER_CONFIRMATION(ORDER_ID)
        DISPLAY "Siparişiniz alındı. Teşekkür ederiz!"
    ELSE
        DISPLAY "Ödeme başarısız. Lütfen tekrar deneyin."
        TERMINATE_SESSION()
        RETURN
    ENDIF

    DISPLAY "Sipariş Numaranız: " + ORDER_ID
    DISPLAY "Tahmini Teslimat: 2-5 iş günü"
    
    TERMINATE_SESSION()

END Online_Shopping_Session
