BEGIN ATM_Withdraw_Process

    INITIALIZE ATM
    DISPLAY "Kart Takınız"

    WAIT_FOR_CARD_INSERTION()
    IF CARD_INSERTED THEN
        READ_CARD()

        IF IS_CARD_VALID() THEN
            FOR pin_attempt IN 1 TO 3 DO
                pin = PROMPT_FOR_PIN()
                IF VERIFY_PIN(pin) THEN
                    GOTO WithdrawFlow
                ELSE
                    DISPLAY "Hatalı PIN"

            IF pin_attempt == 3 THEN
                DISPLAY "Kart bloke edildi"
                BLOCK_CARD()
                EJECT_CARD()
                TERMINATE_SESSION()
                RETURN
        ELSE
            DISPLAY "Geçersiz kart"
            EJECT_CARD()
            TERMINATE_SESSION()
            RETURN

    ELSE
        LOOP TO WAIT_FOR_CARD_INSERTION

WithdrawFlow:

    account = PROMPT_SELECT_ACCOUNT()
    amount = PROMPT_ENTER_AMOUNT()

    IF NOT IS_BALANCE_SUFFICIENT(account, amount) OR
       NOT IS_WITHIN_DAILY_LIMIT(account, amount) OR
       NOT IS_ATM_CASH_AVAILABLE(amount) THEN
        DISPLAY "Yetersiz bakiye veya limit"
        EJECT_CARD()
        TERMINATE_SESSION()
        RETURN

    IF NOT AUTHORIZE_WITH_HOST(account, amount) THEN
        DISPLAY "Banka onayı alınamadı"
        EJECT_CARD()
        TERMINATE_SESSION()
        RETURN

    distribution = CALCULATE_DENOMINATION(amount)
    IF distribution == NULL THEN
        DISPLAY "Uygun banknot dağılımı yok"
        IF USER_WANTS_TO_TRY_DIFFERENT_AMOUNT() THEN
            GOTO WithdrawFlow  // yeniden miktar girme
        ELSE
            DISPLAY "İşlem iptal edildi"
            EJECT_CARD()
            TERMINATE_SESSION()
            RETURN
    ENDIF

    IF DISPENSE_CASH(distribution) THEN
        IF FINALIZE_WITH_HOST(account, amount) THEN
            PRINT_RECEIPT(account, amount)
        ELSE
            DISPLAY "Banka işlem sonrası bildirimi başarısız"
        ENDIF
    ELSE
        DISPLAY "Para verme hatası"
        EJECT_CARD()
        TERMINATE_SESSION()
        RETURN
    ENDIF

    EJECT_CARD()
    TERMINATE_SESSION()
    RETURN

ON_SESSION_TIMEOUT:
    DISPLAY "Oturum zaman aşımına uğradı"
    EJECT_CARD()
    TERMINATE_SESSION()
    RETURN

END ATM_Withdraw_Process
