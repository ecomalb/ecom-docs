# Value actionCode, responseCode


<table data-full-width="true" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>code</th>
      <th>content</th>
      <th>actioncode</th>
      <th>responsecode</th>
      <th>cb_txn_action_code</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>approved</td>
      <td>Успішно</td>
      <td>0</td>
      <td>00</td>
      <td>authorisationApproved</td>
    </tr>
    <tr>
      <td>honourWithId</td>
      <td>Схвалено з ідентифікатором</td>
      <td>0</td>
      <td>01</td>
      <td>authorisationApproved</td>
    </tr>
    <tr>
      <td>approvalForPartialAmt</td>
      <td>Схвалення часткової суми</td>
      <td>0</td>
      <td>02</td>
      <td>authorisationApproved</td>
    </tr>
    <tr>
      <td>approvedVip</td>
      <td>Схвалено, VIP</td>
      <td>0</td>
      <td>03</td>
      <td>authorisationApproved</td>
    </tr>
    <tr>
      <td>approvedUpdateT3</td>
      <td>Схвалено, оновити T3</td>
      <td>0</td>
      <td>04</td>
      <td>authorisationApproved</td>
    </tr>
    <tr>
      <td>approvedAccountTypeSpecified</td>
      <td>Схвалено, тип рахунку вказано емітентом картки</td>
      <td>0</td>
      <td>05</td>
      <td>authorisationApproved</td>
    </tr>
    <tr>
      <td>approvedForPartialAmount</td>
      <td>Схвалено часткову суму, тип рахунку вказано емітентом картки</td>
      <td>0</td>
      <td>06</td>
      <td>authorisationApproved</td>
    </tr>
    <tr>
      <td>approvedUpdateIcc</td>
      <td>Схвалено, оновити ICC</td>
      <td>0</td>
      <td>07</td>
      <td>authorisationApproved</td>
    </tr>
    <tr>
      <td>iccOfflineApproved</td>
      <td>Схвалено офлайн ICC</td>
      <td>0</td>
      <td>80</td>
      <td>authorisationApproved</td>
    </tr>
    <tr>
      <td>iccUnableOnlineApproved</td>
      <td>ICC не може вийти онлайн, схвалено</td>
      <td>0</td>
      <td>81</td>
      <td>authorisationApproved</td>
    </tr>
    <tr>
      <td>iccApprovedInitiatedReferralAar</td>
      <td>Запит балансу</td>
      <td>0</td>
      <td>82</td>
      <td>authorisationApproved</td>
    </tr>
    <tr>
      <td>purchaseApprovedOnlyTxnCode09</td>
      <td>Сума покупки схвалена (без кешбеку) для txncode 09</td>
      <td>0</td>
      <td>83</td>
      <td>authorisationApproved</td>
    </tr>
    <tr>
      <td>authorisationDeniedDoNotHonour</td>
      <td>Не обслуговувати або відхилити без пояснення</td>
      <td>1</td>
      <td>00</td>
      <td>authorisationDenied</td>
    </tr>
    <tr>
      <td>authorisationDeniedCardExpired</td>
      <td>Термін дії картки закінчився</td>
      <td>1</td>
      <td>01</td>
      <td>authorisationDenied</td>
    </tr>
    <tr>
      <td>suspectedFrau</td>
      <td>Підозра на шахрайство</td>
      <td>1</td>
      <td>02</td>
      <td>authorisationDenied</td>
    </tr>
    <tr>
      <td>authorisationDeniedAcceptorContactAcquirer</td>
      <td>Відхилено, зв’яжіться з продавцем/еквайєром</td>
      <td>1</td>
      <td>03</td>
      <td>authorisationDenied</td>
    </tr>
    <tr>
      <td>authorisationDeniedRestrictedCard</td>
      <td>Обмежена картка</td>
      <td>1</td>
      <td>04</td>
      <td>authorisationDenied</td>
    </tr>
    <tr>
      <td>authorisationDeniedAcceptorContactSecurityDpt</td>
      <td>Відхилено, зверніться до еквайєра або постачальника послуг</td>
      <td>1</td>
      <td>05</td>
      <td>authorisationDenied</td>
    </tr>
    <tr>
      <td>authorisationDeniedPinTriesExceeded</td>
      <td>Перевищено кількість спроб введення PIN</td>
      <td>1</td>
      <td>06</td>
      <td>authorisationDenied</td>
    </tr>
    <tr>
      <td>acceptorContactIssuer</td>
      <td>Відхилено, зверніться до банку-емітента</td>
      <td>1</td>
      <td>07</td>
      <td>authorisationDenied</td>
    </tr>
    <tr>
      <td>referIssuerSpecialCond</td>
      <td>Відхилено, зверніться до банку-емітента</td>
      <td>1</td>
      <td>08</td>
      <td>authorisationDenied</td>
    </tr>
    <tr>
      <td>authorisationDeniedInvalidMerchant</td>
      <td>Термінал заблокований / транзакція заборонена для цього типу терміналу</td>
      <td>1</td>
      <td>09</td>
      <td>authorisationDenied</td>
    </tr>
    <tr>
      <td>authorisationDeniedInvalidAmount</td>
      <td>Неправильна сума</td>
      <td>1</td>
      <td>10</td>
      <td>authorisationDenied</td>
    </tr>
    <tr>
      <td>authorisationDeniedInvalidCardNum</td>
      <td>Недійсний номер картки</td>
      <td>1</td>
      <td>11</td>
      <td>authorisationDenied</td>
    </tr>
    <tr>
      <td>pinRequired</td>
      <td>Потрібен PIN-код</td>
      <td>1</td>
      <td>12</td>
      <td>authorisationDenied</td>
    </tr>
    <tr>
      <td>unacceptableFee</td>
      <td>Неприпустима сума комісії</td>
      <td>1</td>
      <td>13</td>
      <td>authorisationDenied</td>
    </tr>
    <tr>
      <td>noAccountSpecifiedType</td>
      <td>Немає рахунку зазначеного типу</td>
      <td>1</td>
      <td>14</td>
      <td>authorisationDenied</td>
    </tr>
    <tr>
      <td>functionNotSupported</td>
      <td>Функція не підтримується</td>
      <td>1</td>
      <td>15</td>
      <td>authorisationDenied</td>
    </tr>
    <tr>
      <td>authorisationDeniedInsufficientFunds</td>
      <td>Недостатньо коштів</td>
      <td>1</td>
      <td>16</td>
      <td>authorisationDenied</td>
    </tr>
    <tr>
      <td>authorisationDeniedBadPin</td>
      <td>Неправильний PIN-код</td>
      <td>1</td>
      <td>17</td>
      <td>authorisationDenied</td>
    </tr>
    <tr>
      <td>noCardRecord</td>
      <td>Недійсна картка</td>
      <td>1</td>
      <td>18</td>
      <td>authorisationDenied</td>
    </tr>
    <tr>
      <td>authorisationDeniedTransNotAllowedCardhldr</td>
      <td>Транзакція заборонена для власника картки</td>
      <td>1</td>
      <td>19</td>
      <td>authorisationDenied</td>
    </tr>
    <tr>
      <td>authorisationDeniedTransNotAllowedTerminal</td>
      <td>Транзакція заборонена для терміналу</td>
      <td>1</td>
      <td>20</td>
      <td>authorisationDenied</td>
    </tr>
    <tr>
      <td>authorisationDeniedExceedsAmountLimit</td>
      <td>Перевищено ліміт суми картки</td>
      <td>1</td>
      <td>21</td>
      <td>authorisationDenied</td>
    </tr>
    <tr>
      <td>authorisationDeniedSecurityViolation</td>
      <td>Порушення безпеки</td>
      <td>1</td>
      <td>22</td>
      <td>authorisationDenied</td>
    </tr>
    <tr>
      <td>authorisationDeniedExceedsFrequencyLimit</td>
      <td>Перевищено ліміт кількості транзакцій по картці</td>
      <td>1</td>
      <td>23</td>
      <td>authorisationDenied</td>
    </tr>
    <tr>
      <td>volationOfLaw</td>
      <td>Підозра на порушення закону</td>
      <td>1</td>
      <td>24</td>
      <td>authorisationDenied</td>
    </tr>
    <tr>
      <td>cardNotEffective</td>
      <td>Картка недійсна</td>
      <td>1</td>
      <td>25</td>
      <td>authorisationDenied</td>
    </tr>
    <tr>
      <td>invalidPinBlock</td>
      <td>Неправильний PIN-код</td>
      <td>1</td>
      <td>26</td>
      <td>authorisationDenied</td>
    </tr>
    <tr>
      <td>pinLengthError</td>
      <td>Помилка довжини PIN-коду</td>
      <td>1</td>
      <td>27</td>
      <td>authorisationDenied</td>
    </tr>
    <tr>
      <td>pinKeySyncError</td>
      <td>Помилка синхронізації ключа PIN</td>
      <td>1</td>
      <td>28</td>
      <td>authorisationDenied</td>
    </tr>
    <tr>
      <td>authorisationDeniedSuspectCounterfeit</td>
      <td>Підозра на шахрайство</td>
      <td>1</td>
      <td>29</td>
      <td>authorisationDenied</td>
    </tr>
    <tr>
      <td>noAcquirerService</td>
      <td>Зверніться до еквайєра</td>
      <td>1</td>
      <td>64</td>
      <td>authorisationDenied</td>
    </tr>
    <tr>
      <td>notFulfillAmlRequirements</td>
      <td>Порушення правил AML</td>
      <td>1</td>
      <td>65</td>
      <td>authorisationDenied</td>
    </tr>
    <tr>
      <td>incorrectRecipientPan</td>
      <td>Неправильна картка отримувача</td>
      <td>1</td>
      <td>66</td>
      <td>authorisationDenied</td>
    </tr>
    <tr>
      <td>cardholderContactIssuer</td>
      <td>Відхилено. Зверніться до емітента</td>
      <td>1</td>
      <td>70</td>
      <td>authorisationDenied</td>
    </tr>
    <tr>
      <td>pinNotChanged</td>
      <td>PIN не змінено</td>
      <td>1</td>
      <td>71</td>
      <td>authorisationDenied</td>
    </tr>
    <tr>
      <td>icc1stGenAcFailed</td>
      <td>Помилка даних чипа</td>
      <td>1</td>
      <td>72</td>
      <td>authorisationDenied</td>
    </tr>
    <tr>
      <td>invalidTrackData</td>
      <td>Помилка даних картки</td>
      <td>1</td>
      <td>73</td>
      <td>authorisationDenied</td>
    </tr>
    <tr>
      <td>exceedsLimit</td>
      <td>Перевищено ліміт</td>
      <td>1</td>
      <td>74</td>
      <td>authorisationDenied</td>
    </tr>
    <tr>
      <td>systemMalfunction</td>
      <td>Перевищено ліміт отриманих/знятих коштів або потрібна перевірка EMV 3DS (для платежів)</td>
      <td>1</td>
      <td>76</td>
      <td>authorisationDenied</td>
    </tr>
    <tr>
      <td>invalidCurrencyCodeAmex</td>
      <td>Неправильний код валюти – AMEX</td>
      <td>1</td>
      <td>77</td>
      <td>authorisationDenied</td>
    </tr>
    <tr>
      <td>iccDeclineCardInitiated</td>
      <td>Помилка даних чипа</td>
      <td>1</td>
      <td>78</td>
      <td>authorisationDenied</td>
    </tr>
    <tr>
      <td>pinChangeDeclined</td>
      <td>Зміна PIN відхилена</td>
      <td>1</td>
      <td>79</td>
      <td>authorisationDenied</td>
    </tr>
    <tr>
      <td>amountNotDivisible</td>
      <td>Неправильна сума</td>
      <td>1</td>
      <td>80</td>
      <td>authorisationDenied</td>
    </tr>
    <tr>
      <td>amountBigAtm</td>
      <td>Сума занадто велика для банкомата</td>
      <td>1</td>
      <td>81</td>
      <td>authorisationDenied</td>
    </tr>
    <tr>
      <td>atmOutCash</td>
      <td>У банкоматі немає готівки</td>
      <td>1</td>
      <td>82</td>
      <td>authorisationDenied</td>
    </tr>
    <tr>
      <td>noChequingAccount</td>
      <td>Немає доступного чекового рахунку</td>
      <td>1</td>
      <td>83</td>
      <td>authorisationDenied</td>
    </tr>
    <tr>
      <td>newPinsEnteredDiffer</td>
      <td>Нові введені PIN-коди не збігаються</td>
      <td>1</td>
      <td>84</td>
      <td>authorisationDenied</td>
    </tr>
    <tr>
      <td>authorisationDeniedCvvValidationError</td>
      <td>Помилка перевірки CVV</td>
      <td>1</td>
      <td>85</td>
      <td>authorisationDenied</td>
    </tr>
    <tr>
      <td>preAuthLimitExceeded</td>
      <td>Перевищено ліміт часу попередньої авторизації</td>
      <td>1</td>
      <td>86</td>
      <td>authorisationDenied</td>
    </tr>
    <tr>
      <td>cardDestroyed</td>
      <td>Картка була знищена</td>
      <td>1</td>
      <td>87</td>
      <td>authorisationDenied</td>
    </tr>
    <tr>
      <td>restrictedCardNoFunds</td>
      <td>Недостатньо коштів</td>
      <td>1</td>
      <td>88</td>
      <td>authorisationDenied</td>
    </tr>
    <tr>
      <td>forexNotAvailable</td>
      <td>Форекс недоступний</td>
      <td>1</td>
      <td>89</td>
      <td>authorisationDenied</td>
    </tr>
    <tr>
      <td>txnCountLimitExceeded</td>
      <td>Перевищено ліміт транзакцій по картці</td>
      <td>1</td>
      <td>90</td>
      <td>authorisationDenied</td>
    </tr>
    <tr>
      <td>systemOverloadRetryPoss</td>
      <td>Система перевантажена. Спробуйте пізніше</td>
      <td>1</td>
      <td>91</td>
      <td>authorisationDenied</td>
    </tr>
    <tr>
      <td>statementDataNotAvail</td>
      <td>Дані виписки недоступні</td>
      <td>1</td>
      <td>92</td>
      <td>authorisationDenied</td>
    </tr>
    <tr>
      <td>authorisationDeniedPinTriesExceeded</td>
      <td>Перевищено кількість спроб введення PIN</td>
      <td>1</td>
      <td>93</td>
      <td>authorisationDenied</td>
    </tr>
    <tr>
      <td>noBalanceDataAvailable</td>
      <td>Дані про баланс недоступні</td>
      <td>1</td>
      <td>94</td>
      <td>authorisationDenied</td>
    </tr>
    <tr>
      <td>iccOfflineDeclined</td>
      <td>Помилка даних чипа</td>
      <td>1</td>
      <td>95</td>
      <td>authorisationDenied</td>
    </tr>
    <tr>
      <td>iccUnableOnlineDeclined</td>
      <td>Помилка даних чипа</td>
      <td>1</td>
      <td>96</td>
      <td>authorisationDenied</td>
    </tr>
    <tr>
      <td>iccCardAuthenticationFailed</td>
      <td>Помилка даних чипа</td>
      <td>1</td>
      <td>97</td>
      <td>authorisationDenied</td>
    </tr>
    <tr>
      <td>noReceiptAvailAtm</td>
      <td>У банкоматі немає доступної квитанції</td>
      <td>1</td>
      <td>98</td>
      <td>authorisationDenied</td>
    </tr>
    <tr>
      <td>noTucNumberAvailabl</td>
      <td>Номер TUC недоступний</td>
      <td>1</td>
      <td>99</td>
      <td>authorisationDenied</td>
    </tr>
    <tr>
      <td>doNotHonour</td>
      <td>Відхилено без пояснення</td>
      <td>2</td>
      <td>00</td>
      <td>authorisationDeniedPickup</td>
    </tr>
    <tr>
      <td>notSupportedReceiver</td>
      <td>Не підтримується отримувачем</td>
      <td>2</td>
      <td>01</td>
      <td>authorisationDeniedPickup</td>
    </tr>
    <tr>
      <td>authorisationDeniedPickupSuspectedFraud</td>
      <td>Підозра на шахрайство</td>
      <td>2</td>
      <td>02</td>
      <td>authorisationDeniedPickup</td>
    </tr>
    <tr>
      <td>acceptorContactAcquirer</td>
      <td>Відхилено, зверніться до еквайєра</td>
      <td>2</td>
      <td>03</td>
      <td>authorisationDeniedPickup</td>
    </tr>
    <tr>
      <td>authorisationDeniedPickupRestrictedCard</td>
      <td>Обмежена картка</td>
      <td>2</td>
      <td>04</td>
      <td>authorisationDeniedPickup</td>
    </tr>
    <tr>
      <td>acceptorContactSecurityDpt</td>
      <td>Порушення безпеки</td>
      <td>2</td>
      <td>05</td>
      <td>authorisationDeniedPickup</td>
    </tr>
    <tr>
      <td>pinTriesExceeded</td>
      <td>Перевищено кількість спроб введення PIN</td>
      <td>2</td>
      <td>06</td>
      <td>authorisationDeniedPickup</td>
    </tr>
    <tr>
      <td>specialConditions</td>
      <td>Відхилено за спеціальних умов</td>
      <td>2</td>
      <td>07</td>
      <td>authorisationDeniedPickup</td>
    </tr>
    <tr>
      <td>lostCard</td>
      <td>Втрачена картка</td>
      <td>2</td>
      <td>08</td>
      <td>authorisationDeniedPickup</td>
    </tr>
    <tr>
      <td>stolenCard</td>
      <td>Вкрадена картка</td>
      <td>2</td>
      <td>09</td>
      <td>authorisationDeniedPickup</td>
    </tr>
    <tr>
      <td>suspectCounterfeit</td>
      <td>Підозра на підробку</td>
      <td>2</td>
      <td>10</td>
      <td>authorisationDeniedPickup</td>
    </tr>
    <tr>
      <td>cvvValidationError</td>
      <td>Помилка перевірки CVV</td>
      <td>2</td>
      <td>85</td>
      <td>authorisationDeniedPickup</td>
    </tr>
    <tr>
      <td>reversalChargebackActionsAccepted</td>
      <td>Прийнято до обробки</td>
      <td>4</td>
      <td>00</td>
      <td>reversalChargebackActions</td>
    </tr>
    <tr>
      <td>acceptedNoFinancialLiab</td>
      <td>Прийнято до обробки</td>
      <td>9</td>
      <td>00</td>
      <td>errorResponseAction</td>
    </tr>
    <tr>
      <td>acceptedFinLiabiltyAcc</td>
      <td>Прийнято до обробки</td>
      <td>9</td>
      <td>01</td>
      <td>errorResponseAction</td>
    </tr>
    <tr>
      <td>invalidTransaction</td>
      <td>Неправильна транзакція</td>
      <td>9</td>
      <td>02</td>
      <td>errorResponseAction</td>
    </tr>
    <tr>
      <td>reEnterTransaction</td>
      <td>Відхилено. Повторіть транзакцію</td>
      <td>9</td>
      <td>03</td>
      <td>errorResponseAction</td>
    </tr>
    <tr>
      <td>formatError</td>
      <td>Помилка формату даних</td>
      <td>9</td>
      <td>04</td>
      <td>errorResponseAction</td>
    </tr>
    <tr>
      <td>acquirerNotSupported</td>
      <td>Еквайєр не підтримується</td>
      <td>9</td>
      <td>05</td>
      <td>errorResponseAction</td>
    </tr>
    <tr>
      <td>cutoverInProgress</td>
      <td>Технічне обслуговування</td>
      <td>9</td>
      <td>06</td>
      <td>errorResponseAction</td>
    </tr>
    <tr>
      <td>issuerSwitchInoperatiive</td>
      <td>Емітент/MPS не відповідає</td>
      <td>9</td>
      <td>07</td>
      <td>errorResponseAction</td>
    </tr>
    <tr>
      <td>destinationNotFound</td>
      <td>Емітент/MPS не визначений</td>
      <td>9</td>
      <td>08</td>
      <td>errorResponseAction</td>
    </tr>
    <tr>
      <td>systemMalfunction</td>
      <td>Системна помилка</td>
      <td>9</td>
      <td>09</td>
      <td>errorResponseAction</td>
        </tr>
        <tr>
      <td>issuerSignedOff</td>
      <td>Емітент недоступний</td>
      <td>9</td>
      <td>10</td>
      <td>errorResponseAction</td>
        </tr>
        <tr>
      <td>issuerTimedOut</td>
      <td>Емітент недоступний</td>
      <td>9</td>
      <td>11</td>
      <td>errorResponseAction</td>
        </tr>
        <tr>
      <td>issuerUnavailable</td>
      <td>Емітент недоступний</td>
      <td>9</td>
      <td>12</td>
      <td>errorResponseAction</td>
        </tr>
        <tr>
      <td>duplicateTransaction</td>
      <td>Дубльована транзакція</td>
      <td>9</td>
      <td>13</td>
      <td>errorResponseAction</td>
        </tr>
        <tr>
      <td>unableTraceOriginalTxn</td>
      <td>Оригінальна транзакція не знайдена</td>
      <td>9</td>
      <td>14</td>
      <td>errorResponseAction</td>
        </tr>
        <tr>
      <td>errorResponseActionReconciliationChkpntError</td>
      <td>Помилка звірки статусу транзакції</td>
      <td>9</td>
      <td>15</td>
      <td>errorResponseAction</td>
        </tr>
        <tr>
      <td>errorResponseActionMacIncorrect</td>
      <td>Криптографічна помилка</td>
      <td>9</td>
      <td>16</td>
      <td>errorResponseAction</td>
        </tr>
        <tr>
      <td>errorResponseActionMacKeySyncError</td>
      <td>Криптографічна помилка</td>
      <td>9</td>
      <td>17</td>
      <td>errorResponseAction</td>
        </tr>
        <tr>
      <td>errorResponseActionNoCommsKeysAvail</td>
      <td>Криптографічна помилка</td>
      <td>9</td>
      <td>18</td>
      <td>errorResponseAction</td>
        </tr>
        <tr>
      <td>errorResponseActionEncryptionKeySyncError</td>
      <td>Криптографічна помилка</td>
      <td>9</td>
      <td>19</td>
      <td>errorResponseAction</td>
        </tr>
        <tr>
      <td>errorResponseActionSecurityErrorTryAgain</td>
      <td>Криптографічна помилка</td>
      <td>9</td>
      <td>20</td>
      <td>errorResponseAction</td>
        </tr>
        <tr>
      <td>errorResponseActionSecurityErrorNoAction</td>
      <td>Криптографічна помилка</td>
      <td>9</td>
      <td>21</td>
      <td>errorResponseAction</td>
        </tr>
        <tr>
      <td>messageOutOfSequence</td>
      <td>Помилка номера транзакції</td>
      <td>9</td>
      <td>22</td>
      <td>errorResponseAction</td>
        </tr>
        <tr>
      <td>requestInProgress</td>
      <td>Запит у процесі</td>
      <td>9</td>
      <td>23</td>
      <td>errorResponseAction</td>
        </tr>
        <tr>
      <td>invalidDateTime</td>
      <td>Помилка тайм-ауту виконання транзакції</td>
      <td>9</td>
      <td>40</td>
      <td>errorResponseAction</td>
        </tr>
        <tr>
      <td>disagreement</td>
      <td>Порушення умов</td>
      <td>9</td>
      <td>50</td>
      <td>errorResponseAction</td>
        </tr>
        <tr>
      <td>cardExpired</td>
      <td>Термін дії картки закінчився</td>
      <td>9</td>
      <td>51</td>
      <td>errorResponseAction</td>
        </tr>
        <tr>
      <td>suspectedFraud</td>
      <td>Підозра на шахрайство</td>
      <td>9</td>
      <td>52</td>
      <td>errorResponseAction</td>
        </tr>
        <tr>
      <td>restrictedCard</td>
      <td>Обмежена картка</td>
      <td>9</td>
      <td>53</td>
      <td>errorResponseAction</td>
        </tr>
        <tr>
      <td>invalidMerchant</td>
      <td>Недійсний/заблокований продавець</td>
      <td>9</td>
      <td>54</td>
      <td>errorResponseAction</td>
        </tr>
        <tr>
      <td>invalidAmount</td>
      <td>Недійсна сума</td>
      <td>9</td>
      <td>55</td>
      <td>errorResponseAction</td>
        </tr>
        <tr>
      <td>invalidCardNum</td>
      <td>Недійсний номер картки</td>
      <td>9</td>
      <td>56</td>
      <td>errorResponseAction</td>
        </tr>
        <tr>
      <td>inacceptableFee</td>
      <td>Неприпустима сума комісії</td>
      <td>9</td>
      <td>57</td>
      <td>errorResponseAction</td>
        </tr>
        <tr>
      <td>insufficientFunds</td>
      <td>Недостатньо коштів</td>
      <td>9</td>
      <td>58</td>
      <td>errorResponseAction</td>
        </tr>
        <tr>
      <td>badPin</td>
      <td>Неправильний PIN</td>
      <td>9</td>
      <td>59</td>
      <td>errorResponseAction</td>
        </tr>
        <tr>
      <td>transNotAllowedCardhldr</td>
      <td>Транзакція заборонена для власника картки</td>
      <td>9</td>
      <td>60</td>
      <td>errorResponseAction</td>
        </tr>
        <tr>
      <td>transNotAllowedTerminal</td>
      <td>Транзакція заборонена для терміналу</td>
      <td>9</td>
      <td>61</td>
      <td>errorResponseAction</td>
        </tr>
        <tr>
      <td>exceedsAmountLimit</td>
      <td>Перевищено ліміт суми</td>
      <td>9</td>
      <td>62</td>
      <td>errorResponseAction</td>
        </tr>
        <tr>
      <td>securityViolation</td>
      <td>Порушення безпеки</td>
      <td>9</td>
      <td>63</td>
      <td>errorResponseAction</td>
        </tr>
        <tr>
      <td>exceedsFrequencyLimit</td>
      <td>Перевищено ліміт кількості транзакцій по картці</td>
      <td>9</td>
      <td>64</td>
      <td>errorResponseAction</td>
        </tr>
        <tr>
      <td>violationOfLaw</td>
      <td>Підозра на порушення закону</td>
      <td>9</td>
      <td>65</td>
      <td>errorResponseAction</td>
        </tr>
        <tr>
      <td>reconciliationChkpntError</td>
      <td>Криптографічна помилка</td>
      <td>9</td>
      <td>66</td>
      <td>errorResponseAction</td>
        </tr>
        <tr>
      <td>macIncorrect</td>
      <td>Криптографічна помилка</td>
      <td>9</td>
      <td>67</td>
      <td>errorResponseAction</td>
        </tr>
        <tr>
      <td>macKeySyncError</td>
      <td>Криптографічна помилка</td>
      <td>9</td>
      <td>68</td>
      <td>errorResponseAction</td>
        </tr>
        <tr>
      <td>noCommsKeysAvail</td>
      <td>Криптографічна помилка</td>
      <td>9</td>
      <td>69</td>
      <td>errorResponseAction</td>
        </tr>
        <tr>
      <td>encryptionKeySyncError</td>
      <td>Криптографічна помилка</td>
      <td>9</td>
      <td>70</td>
      <td>errorResponseAction</td>
        </tr>
        <tr>
      <td>securityErrorTryAgain</td>
      <td>Криптографічна помилка</td>
      <td>9</td>
      <td>71</td>
      <td>errorResponseAction</td>
        </tr>
        <tr>
      <td>securityErrorNoAction</td>
      <td>Криптографічна помилка</td>
      <td>9</td>
      <td>72</td>
      <td>errorResponseAction</td>
        </tr>
        <tr>
      <td>messageOutSequence</td>
      <td>Помилка номера транзакції</td>
      <td>9</td>
      <td>73</td>
      <td>errorResponseAction</td>
        </tr>
    <tr>
      <td>Card authentication failed</td>
      <td>Помилка автентифікації картки</td>
      <td>33</td>
      <td>01</td>
      <td>NaN</td>
    </tr>
    <tr>
      <td>Unknown Device</td>
      <td>Система не розпізнає або не підтримує пристрій</td>
      <td>33</td>
      <td>02</td>
      <td>NaN</td>
    </tr>
    <tr>
      <td>Unsupported Device</td>
      <td>Система не підтримує тип пристрою</td>
      <td>33</td>
      <td>03</td>
      <td>NaN</td>
    </tr>
    <tr>
      <td>Exceeds authentication frequency limit</td>
      <td>Перевищено кількість спроб автентифікації</td>
      <td>33</td>
      <td>04</td>
      <td>NaN</td>
    </tr>
    <tr>
      <td>Expired card</td>
      <td>Термін дії картки закінчився</td>
      <td>33</td>
      <td>05</td>
      <td>NaN</td>
    </tr>
    <tr>
      <td>Invalid card number</td>
      <td>Неправильний номер картки</td>
      <td>33</td>
      <td>06</td>
      <td>NaN</td>
    </tr>
    <tr>
      <td>Invalid transaction</td>
      <td>Неправильна транзакція</td>
      <td>33</td>
      <td>07</td>
      <td>NaN</td>
    </tr>
    <tr>
      <td>No card record</td>
      <td>Недійсна картка</td>
      <td>33</td>
      <td>08</td>
      <td>NaN</td>
    </tr>
    <tr>
      <td>Security failure</td>
      <td>Помилка безпеки</td>
      <td>33</td>
      <td>09</td>
      <td>NaN</td>
    </tr>
    <tr>
      <td>Stolen card</td>
      <td>Картка вкрадена</td>
      <td>33</td>
      <td>10</td>
      <td>NaN</td>
    </tr>
    <tr>
      <td>Suspected fraud</td>
      <td>Підозра на шахрайство</td>
      <td>33</td>
      <td>11</td>
      <td>NaN</td>
    </tr>
    <tr>
      <td>Transaction not permitted to cardholder</td>
      <td>Транзакція заборонена для власника картки</td>
      <td>33</td>
      <td>12</td>
      <td>NaN</td>
    </tr>
    <tr>
      <td>Cardholder not enrolled in service</td>
      <td>Власник картки не зареєстрований у 3D Secure</td>
      <td>33</td>
      <td>13</td>
      <td>NaN</td>
    </tr>
    <tr>
      <td>Transaction timed out at the ACS</td>
      <td>Тайм-аут транзакції на ACS</td>
      <td>33</td>
      <td>14</td>
      <td>NaN</td>
        </tr>
        <tr>
      <td>Low confidence</td>
      <td>Низька впевненість у транзакції</td>
      <td>33</td>
      <td>15</td>
      <td>NaN</td>
        </tr>
        <tr>
      <td>Medium confidence</td>
      <td>Середня впевненість у транзакції</td>
      <td>33</td>
      <td>16</td>
      <td>NaN</td>
        </tr>
        <tr>
      <td>High confidence</td>
      <td>Висока впевненість у транзакції</td>
      <td>33</td>
      <td>17</td>
      <td>NaN</td>
        </tr>
        <tr>
      <td>Very High confidence</td>
      <td>Дуже висока впевненість у транзакції</td>
      <td>33</td>
      <td>18</td>
      <td>NaN</td>
        </tr>
        <tr>
      <td>Exceeds ACS maximum challenges</td>
      <td>Перевищено максимальну кількість викликів ACS</td>
      <td>33</td>
      <td>19</td>
      <td>NaN</td>
        </tr>
        <tr>
      <td>Non-Payment transaction not supported</td>
      <td>Транзакції без оплати не підтримуються</td>
      <td>33</td>
      <td>20</td>
      <td>NaN</td>
        </tr>
        <tr>
      <td>3RI transaction not supported</td>
      <td>Транзакція не підтримується емітентом</td>
      <td>33</td>
      <td>21</td>
      <td>NaN</td>
        </tr>
        <tr>
      <td>ACS technical issue</td>
      <td>Технічна проблема ACS</td>
      <td>33</td>
      <td>22</td>
      <td>NaN</td>
        </tr>
        <tr>
      <td>Decoupled Authentication required by ACS but not requested by 3DS Requestor</td>
      <td>Потрібна повторна автентифікація на ACS</td>
      <td>33</td>
      <td>23</td>
      <td>NaN</td>
        </tr>
        <tr>
      <td>3DS Requestor Decoupled Max Expiry Time exceeded</td>
      <td>Перевищено максимальний час очікування 3DS Requestor</td>
      <td>33</td>
      <td>24</td>
      <td>NaN</td>
        </tr>
        <tr>
      <td>Decoupled Authentication was provided insufficient time to authenticate Cardholder. ACS will not make attempt</td>
      <td>Для автентифікації власника картки було надано недостатньо часу. ACS не буде виконувати автентифікацію.</td>
      <td>33</td>
      <td>25</td>
      <td>NaN</td>
        </tr>
        <tr>
      <td>Authentication attempted but not performed by the Cardholder</td>
      <td>Власник картки спробував автентифікацію, але не завершив її</td>
      <td>33</td>
      <td>26</td>
      <td>NaN</td>
        </tr>
        <tr>
      <td>Preferred Authentication Method not supported</td>
      <td>Бажаний метод автентифікації не підтримується</td>
      <td>33</td>
      <td>27</td>
      <td>NaN</td>
        </tr>
        <tr>
      <td>Validation of content security policy failed</td>
      <td>Помилка перевірки політики безпеки вмісту</td>
      <td>33</td>
      <td>28</td>
      <td>NaN</td>
        </tr>
    <tr>
      <td>Authentication attempted but not completed by the Cardholder. Fall back to Decoupled Authentication</td>
      <td>Власник картки спробував автентифікацію, але не завершив її. Перехід до відокремленої автентифікації</td>
      <td>33</td>
      <td>29</td>
      <td>NaN</td>
    </tr>
    <tr>
      <td>Authentication completed successfully but additional authentication of the Cardholder required. Reinitiate as Decoupled Authentication</td>
      <td>Автентифікація успішно завершена, але потрібна додаткова автентифікація власника картки. Перезапустіть як відокремлену автентифікацію</td>
      <td>33</td>
      <td>30</td>
      <td>NaN</td>
    </tr>
    <tr>
      <td>Reserved for EMVCo future use (values invalid until defined by EMVCo) or for DS use</td>
      <td>Зарезервовано для майбутнього використання EMVCo (значення недійсні, доки не визначені EMVCo) або для використання DS</td>
      <td>33</td>
      <td>31-99</td>
      <td>NaN</td>
    </tr>
    <tr>
      <td>Unknown error 3DS</td>
      <td>Невідома помилка</td>
      <td>33</td>
      <td>100</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
