# spring_annotations_2022_03

Egy export a Spring-es jegyzeteim közül amit az elmúlt években írtam. A fontosabb annotációkat tartalmazza. Hátha valakinek hasznos lesz...

----
Spring
====
## AliasFor

  
min: metódus  
fontosabb paraméterek: String  
Aliasok létrehozásához. (Saját annotációknál). Ha például egy mezőt többféle képpen is nevezhetünk egy annotációban akkor ennek segítségével lehet ezt deifniálni   
  

## Async

  
min: metódus  
fontosabb paraméterek: String  
A metódust aszinkronként kell végrehajtani. A paraméter a TaskExecutor neve amit xmlben kell definiálnunk (Vagy egy TaskExecutor bean-t amit ellátunk egy Qualifier-rel). Ha nem adjuk meg a nevet akkor is kell executort definiálni. A visszatérési érték lehet egy Future  
  

## Autowired

  
min: konstruktor/tagváltozó/metódus  
Injektálási pontot jelöl  
  

## Bean

  
min: metódus  
fontosabb paraméterek: String[] name   
a spring konténer által menedzselt Bean-t ad vissza a függvény (beanekre a megadott nevekkel hivatkozhatunk). Konfigurációs osztályokat nem kell ezzel a módszerrel létrehozni azok (a feltételeknek megfelelően (pl. Profile)) létrejönnek. Ha mégis így csinálunk akkor 2 példány jön létre, és a spring újabb verzióiban (>2.2.2) már hibát fog dobni (van erre assertálás)  
  

## Component

  
min: osztály  
fontosabb paraméterek: String value  
Az osztály egy komponens amit a Spring környezet képes felismerni. A value paraméterrel megadhatjuk a spring bean nevét  
  

## ComponentScan

  
min: osztály  
fontosabb paraméterek: Class<?>[] basePackageClasses, String[] basePackages  
@Component osztályra. A megadott csomagokban további @Component-eket keres, és létrehozza a bean-eket a @Bean-jeivel. Nagy alkalmazás esetében nagyon be tudja lassítani annak létrehozását. Ebben az esetben használjunk inkább @Import-ot. Általában az Application osztályra szokás rakni (ami elindítja az alkalmazást). Használhatjuk az egyes tesztesetek futtatásánál a bean-ek létrehoásához (csak azt ami kell a teszthez, ilyenkor általában kell mellé a @AutoConfigureMockMvc is)  
  

## Conditional

  
min: osztály/metódus  
fontosabb paraméterek: Class<? extends Condition>[] value  
Csak akkor engedélyezi a komponens regisztrációját, ha megfelel az összes feltételnek. Saját feltételeket ez alapján tudunk leellenőrizni  
  

## ConditionalOnBean

  
min: osztály  
fontosabb paraméterek: class  
Egy bean létrehozását egy másik bean létezésétől tehetünk függővé  
ref: [[1]](https://www.baeldung.com/spring-conditional-annotations)  

## ConditionalOnClass

  
min: osztály  
fontosabb paraméterek: Class  
Olyan Conditional ami megnézi, hogy a classpathban benne van-e a megadott class  
  

## ConditionalOnExpression

  
min: osztály  
fontosabb paraméterek: String value  
Konfigurációs osztályra tehető. Olyan mint ha profile-t használnánk, csak bármilyen feltételt megadhatunk. A paramétere egy expression language kifejezés.  
ref: [[1]](https://docs.spring.io/spring-boot/docs/current/api/org/springframework/boot/autoconfigure/condition/ConditionalOnExpression.html)  

## ConditionalOnJava

  
min: osztály  
fontosabb paraméterek: JavaVersion  
A bean létrehozását a java verziójától tudjuk függővé tenni  
ref: [[1]](https://www.baeldung.com/spring-conditional-annotations)  

## ConditionalOnMissingBean

  
min: osztály/metódus  
fontosabb paraméterek: String[] name, Class<?>[] value  
@Bean metódusokra kell rakni. Akkor hozza létre a bean-t, ha még nincs ilyen névvel rendelkező definiálva. A Spring AutoConfiguration ez alapján működik (entityManagerFactory, transactionManager-t ez alapján hozza létre)   
ref: [[1]](https://docs.spring.io/spring-boot/docs/current/api/org/springframework/boot/autoconfigure/condition/ConditionalOnMissingBean.html)  

## ConditionalOnProperty

  
min: osztály/metódus  
fontosabb paraméterek: String prefix, String[] name, String []value, boolean matchIfMissing  
Feltételes bean létrehozáshoz. Olyan Conditional ami a tulajdonságok értékét nézi. A tulajdonságoknak benn kell lenniük az Environment-ben (a matchIfMissing ez kikapcsolható). Leellenőrizhetjük pl, hogy az érték a megfelelő prefix-szel kezdődik. Megadhatjuk, hogy mely tulajdonságokat engedélyezzen.   
ref: [[1]](https://www.baeldung.com/spring-conditionalonproperty)  

## ConditionalOnWarDeployment

  
min: osztály  
A bean létrehozását a deployment módjától tudjuk függővé tenni. (Ha alkalmazás szerverre telepítjük)  
ref: [[1]](https://docs.spring.io/spring-boot/docs/current/api/org/springframework/boot/autoconfigure/condition/ConditionalOnWarDeployment.html)  

## Configurable

  
min: osztály  
fontosabb paraméterek: boolean	preConstruction  
Az osztályt injektációra jelöli. (Injektálni lehet bele serviceket, akár entitásokra is rakható)(Ennek a hatásához kell a aspectj-maven-plugin, és a spring-aspects dependency is, és egy @EnableSpringConfigured az egyik osztályon)  
ref: [[1]](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/beans/factory/annotation/Configurable.html)  

## Configuration

  
min: osztály  
Jelzi, hogy az osztálynak vannak Bean annotációjú metódusai(lehet xmlben is definiálni)  
ref: [[1]](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/context/annotation/Configuration.html)  

## ConfigurationProperties

  
min: osztály  
fontosabb paraméterek: String  
Megadhatunk vele egy konfigurációs tulajdonság osztályt (bean-t). A bean tagváltozóiba a megadott String prefix-szel rendelkező tulajdonságokat fogja betölteni. Ha a projektehz hozzáadjuk a spring-boot-configuration-processor maven dependency-t akkor az a buildelénél plusz konfigokat fog létrehozni a (javadoc alapján) amit az intelliJ képes megjeleníteni  
ref: [[1]](https://www.baeldung.com/intellij-resolve-spring-boot-configuration-properties)  

## ConstructorBinding

  
min: osztály  
A bean tulajdonságait a konstruktorán keresztül töltjük fel. A @ConfigurationProperties-el szokás együtt használni  
ref: [[1]](https://docs.spring.io/spring-boot/docs/current/reference/html/spring-boot-features.html#boot-features-external-config-constructor-binding)  

## ContextConfiguration

  
min: osztály  
fontosabb paraméterek: String[] locations, Class[] classes  
Integrációs tesztekhez megadhatunk konfigurációt. A locations paraméter konfigurációs xml-ekre mutathat, a classes pedig olyan osztrályra ami ApplicationContext-et létrehozza  
  

## ControllerAdvide

  
min: osztály  
fontosabb paraméterek: String[] basePackages, Class<? extends Annotation>[] annotations  
Exception handlert tudunk vele (és az @ExceptionHandler annotációval) készíteni. Meghatározhatjuk, hogy milyen csomagban lévő, vagy milyen annotációval ellátot osztályokban keletkező kivételeket kapjunk el vele.   
ref: [[1]](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/web/bind/annotation/ControllerAdvice.html)  

## DependsOn

  
min: osztály/metódus  
fontosabb paraméterek: String  
A beanünk függ egy másik bean-től  
  

## DirtiesContext

  
min: metódus  
Spring-es tesztnél reseteli a contextet. Tesztre kell rakni, aminek a futtatása előtt törli az ApplicationContext-et.  
ref: [[1]](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/test/annotation/DirtiesContext.html)  

## DynamicPropertySource

  
min: metódus  
A tesztekhez dinamikus tulajdonságokat hozhatunk létre. A metódusnak egy DynamicPropertySource paramétert adhatunk amin keresztül beregisztrálhatjuk a property-ket  
ref: [[1]](https://www.baeldung.com/spring-dynamicpropertysource)  

## EnableAsync

  
min: osztály  
Engedélyezi az aszinkron végrehajtást, AsyncConfigurer interfész implementálásával lehet testreszabni a viselkedését  
  

## EnableAutoConfiguration

  
min: osztály  
fontosabb paraméterek: Class<?>[] exclude  
Engedélyezi auto-konfigurációt. Ehhez figyelembe veszi, hogy mi van a classpath-on, és intelligens módon létrehozza a szükséges bean-eket  
ref: [[1]](https://docs.spring.io/spring-boot/docs/current/api/org/springframework/boot/autoconfigure/EnableAutoConfiguration.html)  

## EnableConfigurationProperties

  
min: osztály  
A @Configuration konfigurációs osztályokon @Profile-t is kell használni.  
ref: [[1]](https://docs.spring.io/spring-boot/docs/current/reference/html/spring-boot-features.html#boot-features-profiles)  

## EnableLoadTimeWeaving

  
min: osztályra (LoadTimeWeavingConfigurer-ből származik)  
Az aspektusok létrehozásának módját állíthatjuk be vele: ezzel betöltés közben jönnek létre (módosul a classfile  
ref: [[1]](https://docs.spring.io/spring/docs/current/javadoc-api/org/springframework/context/annotation/EnableLoadTimeWeaving.html)  

## EnableSpringConfigured

  
min: osztály  
Engedélyezi az AspectJ weaving-et amivel nem bean osztályokba is lehet szervizeket injektálni  
ref: [[1]](https://www.baeldung.com/spring-inject-bean-into-unmanaged-objects)  

## EnableTransactionManagement

  
min: osztályra (@Configuration)  
fontosabb paraméterek: AdviceMode mode  
Beállíthatjuk a tranzakció kezelés módját: Aspektusokon(AspectJ) keresztül, vagy Proxy osztályokon keresztül  
ref: [[1]](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/transaction/annotation/EnableTransactionManagement.html)  

## Import

  
min: osztály  
fontosabb paraméterek: Class  
Konfigurációs osztályra rakjuk, paramétere egy másik konfigurációs osztály. Beimportálja a másik konfigurációs osztály bean-jeit  
  

## ImportResource

  
min: osztály  
fontosabb paraméterek: String[] value  
Bean definíciókat tartalmazó fájlokat(xml) importál be  
  

## Lazy

  
min: osztály  
fontosabb paraméterek: boolean  
Körkörös hivatkozásból adódó versenyhelyzetet oldhatunk fel vele beanek között. Ha false akkor letilthatjuk vele a lazy inicializálást  
ref: [[1]](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/context/annotation/Lazy.html)  

## NonNullApi

  
min: csomagra  
Csomag szinten definiálja, hogy nem fogadunk el, és nem adunk vissza null-t. Nullable-el tudunk metódus szinten testreszabni. package-info.java fájlba kell rakni  
ref: [[1]](https://www.baeldung.com/java-package-info)  

## NonNullFields

  
min: csomagra  
Csomag szinten definiálhatjuk, hogy nem fogadunk el null-t a tagváltozóink értékének. package-info.java fájlba kell rakni  
ref: [[1]](https://www.baeldung.com/java-package-info)  

## Nullable

  
min: metódus/paraméter/tagváltozó  
Az (visszatérési)érték/paraméter lehet null. Egy hint-et ad statikus kódanalizátoroknak (FindBugs)  
  

## Order

  
min: osztály/metódus  
fontosabb paraméterek: int  
A Bean létrejöttének sorrendjét adhatjuk megvele. Habár az annotációt metódusra is lehet rakni, csak akkor érvényesül a hatása ha osztályra tettük.  
  

## org.springframework.cache.annotation.Cacheable

  
min: metódus  
fontosabb paraméterek: String value, String condition  
Bean-ek metódusainak visszatérési értékét tudjuk cache-elni (ha van létrehozott cacheManager-ünk). (Expression Language-ben megírt) feltételes cachelést is tudunk csinálni a condition paraméterrel. Többféle cachelési backendet is tudunk választani. A további testreszabáshoz használjuk az adott cache backend konfigurációs fájljait.  
ref: [[1]](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/cache/annotation/Cacheable.html)  

## org.springframework.transaction.annotation.Transactional

  
min: osztály/metódus  
fontosabb paraméterek: Class<? extends Throwable>[] noRollbackFor, Propagation propagation  
A propagation-nal beállíthatjuk, hogy milyen tranzakcióban fusson a metódus. A propagation = Propagation.REQUIRES_NEW -> új tranzakcióban fusson. Ha egy teszt osztályon használjuk, akkor rollbacke-eli a tranzakciót minden teszt után. Arra vigyázni kell, hogy egy tranzakcionális metódusból, ha ugyanabban az osztályban lévő tranzakciót hívunk meg akkor annak a tranzakciónak ugyanolyan típusúnak kell lennie. Ellenkezö esetben self injection móka.  
ref: [[1]](https://dzone.com/articles/most-common-spring-transactional-mistakes)  

## Primary

  
min: osztály  
@Bean-eknek, és @Configuration-öknek adhatunk meg vele elsődleges beinjektálandó verziót. Hasznos, ha a spring-hez tartozó plugint (pl springfox) akarjuk testreszabni. Ekkor a saját leszármazott osztályunknak fogja beinjektálni  
  

## Profile

  
min: osztály/metódus  
fontosabb paraméterek: String  
Springben profilokat tudunk definiálni a programunkhoz. Ez az annotáció megmondja, hogy csak melyik profilnál legyen betöltve a beanünk. Habár tehetjük metódusra, ez nem ajánlott, mert néha olyan mintha nem értelmezné. Ha külön konfigurációk kellenek akkor inkább az egész osztárlyra (pl. WebMvcConfigurer) rakjuk rá (és csináljunk több konfig osztályt, minthogy a metódusokkal baszakszunk)   
  

## PropertySource

  
min: osztály  
fontosabb paraméterek: String[]  
Config osztályra. properties fájlokat adahatunk meg vele. Az értékek elérhetővé válnak a @Value segítségével.  
  

## Qualifier

  
min: Autowired tagváltozó  
fontosabb paraméterek: String  
Meghatározhatjuk, hogy melyik bean-t injektálja be a Spring az adott helyre. A név ugyan az mint amit megadtunk a @Component vagy @Repository-nál. A változatosság kedvéért ez nem mindig működik  
  

## RequestScope

  
min: osztály/metódus  
Ugyanaz mint a @Scope("request"). Néha valamilyen bug miatt csak olyan @Bean metódusokon működik amik nem várnak más,(@Autowired-es) paramétert  
ref: [[1]](https://docs.spring.io/spring/docs/3.0.0.M3/reference/html/ch04s04.html)  

## Required

  
min: metódus (setter)  
A Bean-ünk setterére kell tenni, ezzel függést határozhatunk meg közöttük amely configuration szakaszban injektálódik (Eager)  
  

## Scheduled

  
min: metódus  
fontosabb paraméterek: int fixedRate, String cron  
Időzített, automatikus végrehajtás. Ahhoz, hogy párhuzamos végrehajtásúvá tegyük, rá kell tennünk az @Async annotációt. Megadhatunk hozzá cron kifejezést is  
ref: [[1]](https://dzone.com/articles/a-guide-to-spring-boot-scheduling)  

## Scope

  
min: metódusra amin van @Bean/osztályra  
fontosabb paraméterek: String  
Megadja a Bean scope-ját;
prototype: minden hivatkozásnál(ApplicationContext-bol lekérés) új példányt hoz létre(stateful)
singleton: egy singleton objektumot hoz létre(containerenként)
session : olyan mint a SessionScoped
request: webes alrendszerhez tartozik, a requesthez hozzárendel egy-et  
ref: [[1]](https://docs.spring.io/spring/docs/3.0.0.M3/reference/html/ch04s04.html)  

## SessionScope

  
min: osztály/metódus  
Ugyanaz mint a @Scope(value = WebApplicationContext.SCOPE_SESSION)  
ref: [[1]](https://www.baeldung.com/spring-bean-scopes)  

## SpringBootApplication

  
min: osztály  
definiálja, hogy melyik osztály a fő spring indító osztály (amelyik tartalmaz main-t). Ekvivalens a Configuration,EnableAutoConfiguration,ComponentScan annotáció hármassal  
  

## TransactionalEventListener

  
min: metódus  
Az eseménykezelő tranzakcionális  
ref: [[1]](https://www.baeldung.com/spring-events)  

## TransactionConfiguration

  
min: osztály  
fontosabb paraméterek: String transactionManager, boolean defaultRollback  
Megadhatjuk a tranzakció managert (név alapján)  
  

## Value

  
min: tagváltozó  
fontosabb paraméterek: String  
Beinjektálja az értéket egy property fájlból a tagváltozóba. Alapértelmezett értéket is megadhatunk neki, ennek formátuma: ${value:defualtValue}
Csak String típusú változóba injektálhatunk vele. Ha konvertálni szeretnénk valamivé akkor egy @PostConstruct-ban a Environment.getProperty-vel kérjük le az értéket  
  

Spring Boot Test
====
## ActiveProfiles

  
min: osztály  
fontosabb paraméterek: String  
Kijelöli, hogy milyen profillal fusson a teszt. Tesztosztályra tehető. Vigyázni kell vele, mert akkor más profilt (pl paraméterben) nem adhatunk meg  
  

## AutoConfigureTestDatabase

  
min: teszt osztály  
megkeres egy test db-t a dependency-k között, és azt fogja használni a Repository-k példányosításánál  
  

## Rollback

  
min: osztály/metódus  
fontosabb paraméterek: boolean  
A teszt után a menedzselt tranzakciót vissza kell-e görgetni  
  

## SpringBootTest

  
min: osztály  
fontosabb paraméterek: Class<?>[] classes  
a classes alapján betölti az adott teszthez a konfigurációt. Ha a classes nincs definiálva, megkeresi a SpringBootConfiguration-t és azt tekinti konfignak  
  

## TestPropertySource

  
min: osztály  
fontosabb paraméterek: String[] properties  
Tulajdonságokat adhatunk meg(application.properties-beli) a teszt futtatásához. @TestPropertySource(locations="classpath:test.properties")  
ref: [[1]](https://reflectoring.io/spring-boot-data-jpa-test/)  

Spring Caching
====
## EnableCaching

  
min: osztály  
engedélyezi a cache-elést. (org.springframework.boot:spring-boot-starter-cache kell hozzá)  
ref: [[1]](https://dzone.com/articles/caching-with-spring-boot-and-hazelcast)  

Spring Cloud
====
## EnableCircuitBreaker

  
min: osztály  
Engedélyezi Hystrix-es circuitBreaker funkcionalitást  
  

## EnableDiscoveryClient

  
min: osztály  
Regisztrálja magát a DiscoveryRegistrybe (működik mindegyik ServiceRegistry implementációval)  
  

## EnableEurekaClient

  
min: osztály  
Ugyanaz mint a EnableDiscoveryClient csak ez csak Eureka-val működik  
  

## EnableEurekaServer

  
min: osztály  
Elindítja az EurekaServert amibe regisztrálni tudjuk a szervizünket (property fájlal testreszabható)  
  

## EnableHystrixDashboard

  
min: osztály  
Hystrix dashboad-ot engedélyezi. (Kell hozzá a dashboard-os maven dependency)  
ref: [[1]](https://dzone.com/articles/implementing-circuit-breaker-pattern-using-spring)  

## EnableZuulProxy

  
min: osztály  
Zuul szervert engedélyezi, amivel el tudja osztani a terhelést (xml-ből testreszabható)  
  

## HystrixCommand

  
min: metódus  
fontosabb paraméterek: String fallbackMethod  
Jelzi, hogy melyik a metódus kritikus(service vagy Component-nek kell lennie az osztálynak). A paraméterével megadhatunk egy tartalék metódus nevét amit vész esetén végrehajt a keretrendszer.  
  

Spring Data
====
## DataJpaTest

  
min: osztály  
fontosabb paraméterek: boolean showSql  
Létrehoz inmemory adatbázist a (integrációs) tesztünk futtatásához, ellenörzi az entitásokat stb. Az adatbázis meg lesz osztva az összes teszt között amelyeken ez az annotáció rajta van. A paraméterével kiirathatjuk a az sql-eket  
ref: [[1]](https://reflectoring.io/spring-boot-data-jpa-test/)  

## EnableJpaAuditing

  
min: osztály  
fontosabb paraméterek: boolean modifyOnCreate, boolean setDates  
Annotáció alapú auditáció engedélyezése.  
ref: [[1]](https://docs.spring.io/spring-data/jpa/docs/current/api/org/springframework/data/jpa/repository/config/EnableJpaAuditing.html)  

## EnableJpaRepositories

  
min: osztály  
fontosabb paraméterek: BootstrapMode, String entityManagerFactoryRef, String transactionManagerRef, String[] basePackages  
JPARepository létrehozását indikáló annotáció. Megadhatjuk, hogy hogyan hozza létre ezeket a Bean-eket (Lazy/Eager). Lazy -> gyorsabban indul az alkalmazás. Nem kell explicit definiálnunk, ha a projektunk a Spring starterből származik. A entityManagerFactoryRef, és transactionManagerRef tulajdonságokkal definiálhatjuk, hogy melyik EntityManagerFactory, és TransactionManager-t használja. A basePackages-sel megadhatjuk, hogy melyik csomagban lévő entitásokat/repository-kat managel-je.  
  

## Modifying

  
min: interfész metódus definíció  
Repository interfész metódusára rakhatjuk, ezzel jelezhetjük, hogy a metódus adatot updatel/hoz létre (Kötelező rárakni).  
  

## org.springframework.data.annotation.Id

  
min: tagváltozó/metódus/annotáció  
Spring Data Id annotációja (reaktív adateléréshez)  
  

## org.springframework.data.relational.core.mapping.Column

  
min: tagváltozó/metódus/annotáció  
fontosabb paraméterek: String  
Az entitás oszlopának nevét adhatjuk meg ami a relációs adatbázisban van.  
  

## Query

  
min: interfész metódus definíció  
fontosabb paraméterek: String value, String countQuery, boolean nativeQuery  
JPQL (vagy natív) queryket adahatunk meg Repository interfészek metódusaihoz. Valamint megahatunk egy countQuery-t is mellé (Pageing-hez). A metódus paramétereire @Param-ot tehetünk aminek segítségével meg lehet adni, hogy a paraméterre hogyan hivatkozunk a query-ben. Ha update/delete akkor kell rá a @Modifying is  
  

## Repository

  
min: osztály  
fontosabb paraméterek: String  
Repository mechanizmus, ha a szervizünk tárolást, visszakérést, keresést valósít meg ezt használjuk  
  

Spring Data REST
====
## Cacheable

  
min: metódus  
fontosabb paraméterek: String  
A metódus értékét elcacheli. A metódusnak egy paramétere van. A paraméter a cache értéke. (Cache providert is kell konfigurálni mellé)  
  

## CacheEvict

  
min: metódus  
fontosabb paraméterek: String key, String value  
Spring Data Rest Repository metódusára kell rakni. A megadott cache-be (value) beteszi a metódus visszatérési értékét a key alapján. A key egy Expression Language kifejezés. A @Cacheable párja.  
ref: [[1]](https://github.com/spring-projects/spring-data-examples/blob/master/jpa/example/src/main/java/example/springdata/jpa/caching/CachingUserRepository.java)  

## CreatedBy

  
min: metódus/tagváltozó  
Ki hozta létre a rekordot. Spring Auditációs megoldás  
ref: [[1]](https://docs.spring.io/spring-data/jpa/docs/1.3.4.RELEASE/reference/html/jpa.repositories.html)  

## CreatedDate

  
min: metódus/tagváltozó  
Lehet Date, DateTime, Long/long Spring Auditációs megoldás  
ref: [[1]](https://docs.spring.io/spring-data/jpa/docs/1.3.4.RELEASE/reference/html/jpa.repositories.html)  

## EntityGraph

  
min: interfész metódus definíció  
fontosabb paraméterek: String[] attributePaths  
A Repository metódusára kell rakni. Ezzel megadhatjuk, hogy milyen EntityGraph-o(ka)t használjon az entitások felolvasásásánál. save-nél nem működik. Jelenleg a hibernate(5.3) ilyenkor nem veszi figyelembe a FetchMode-ot, és mindig JOIN-al próbálja, és ha pageing-et is szeretnénk akkor a memóriában fogja leképezni a kapcsolatokat amitől nagyon lassú, és erőforrás igényes lesz a query  
ref: [[1]](https://www.baeldung.com/spring-data-jpa-named-entity-graphs)  

## HandleAfterCreate

  
min: metódus  
fontosabb paraméterek: -  
Entitás életciklus eseménykezelő. @RepositoryEventHandler-vel ellátott osztályba kell rakni  
  

## HandleAfterDelete

  
min: metódus  
fontosabb paraméterek: -  
Entitás életciklus eseménykezelő. @RepositoryEventHandler-vel ellátott osztályba kell rakni  
  

## HandleAfterLinkDelete

  
min: metódus  
fontosabb paraméterek: -  
Entitás életciklus eseménykezelő. @RepositoryEventHandler-vel ellátott osztályba kell rakni  
  

## HandleAfterLinkSave

  
min: metódus  
fontosabb paraméterek: -  
Entitás életciklus eseménykezelő. @RepositoryEventHandler-vel ellátott osztályba kell rakni  
  

## HandleAfterSave

  
min: metódus  
fontosabb paraméterek: -  
Entitás életciklus eseménykezelő. @RepositoryEventHandler-vel ellátott osztályba kell rakni  
  

## HandleBeforeCreate

  
min: metódus  
fontosabb paraméterek: -  
Entitás életciklus eseménykezelő. @RepositoryEventHandler-vel ellátott osztályba kell rakni  
  

## HandleBeforeDelete

  
min: metódus  
fontosabb paraméterek: -  
Entitás életciklus eseménykezelő. @RepositoryEventHandler-vel ellátott osztályba kell rakni  
  

## HandleBeforeLinkDelete

  
min: metódus  
fontosabb paraméterek: -  
Entitás életciklus eseménykezelő. @RepositoryEventHandler-vel ellátott osztályba kell rakni  
  

## HandleBeforeLinkSave

  
min: metódus  
fontosabb paraméterek: -  
Entitás életciklus eseménykezelő. @RepositoryEventHandler-vel ellátott osztályba kell rakni  
  

## HandleBeforeSave

  
min: metódus  
fontosabb paraméterek: -  
Entitás életciklus eseménykezelő. @RepositoryEventHandler-vel ellátott osztályba kell rakni  
  

## LastModifiedBy

  
min: metódus/tagváltozó (User)  
Ki módosította utóljára. Spring Auditációs megoldás  
ref: [[1]](https://docs.spring.io/spring-data/jpa/docs/1.3.4.RELEASE/reference/html/jpa.repositories.html)  

## LastModifiedDate

  
min: metódus/tagváltozó  
Lehet Date, DateTime, Long/long Spring Auditációs megoldás  
ref: [[1]](https://docs.spring.io/spring-data/jpa/docs/1.3.4.RELEASE/reference/html/jpa.repositories.html)  

## NoRepositoryBean

  
min: interfész  
Nem hogy létre bean-t az interfészből. Akkor érdemes használni, ha a repository-ainknak akarunk egy közös interfészt létrehozni, és abból származtatni a repository-kat  
  

## org.springframework.data.jpa.repository.EntityGraph

  
min: metódus/annotáció  
fontosabb paraméterek: EntityGraphType type, String[] attributePaths  
Vezérelhetjük az objektum gráf lekérdezést vele. (spring data rest kompatibilis). @Query-vel ellátott metódusokra tehetjük  
ref: [[1]](https://docs.spring.io/spring-data/data-jpa/docs/current/api/org/springframework/data/jpa/repository/EntityGraph.html)  

## PageableDefault

  
min: metódus paraméter (Page)  
fontosabb paraméterek: int page, int size  
A page-nek alapértelmezett értékeket állíthatunk be  
  

## Param

  
min: paraméter  
fontosabb paraméterek: String  
JpaRepository-k custom metódusában megahatjuk vele a Paraméter nevét. Előfordulhat, hogy a fordító kéri, hogy a maraméter nevekkel együtt fordítsuk a projektet (-parameters compilerArg)  
  

## Procedure

  
min: metódus  
fontosabb paraméterek: String  
Egy tárolt procedúrát tudunk meghívni vele. Egy JPArepository metódusára lehet tenni. A Paraméter a procedúra neve  
  

## Projection

  
min: interfész  
fontosabb paraméterek: String name, Class<?>[] types  
Ha nem akarjuk egy entitás összes mezőjét visszaadni, ezzel megadhatjuk, hogy melyeket. Az interfész előírja az eredeti entitás getter metódusait amelyeket vissza akarunk adni vagy @Value-val kombinálható. Az entitásnak nem kell implementálnia ezt az interfészt. A Projekciókat az entitások csomagjában kell definiálni  
  

## RepositoryEventHandler

  
min: osztály  
Eseménykezelő osztályt készíthetünk entitásokhoz, ez már képes megkülönböztetni az objektumok típusát (az objetum típusát a kezelő metódusok paraméterei alapján határozza meg, egy eventhandler-be többféle típushoz tartozó kezelő metódust is rakhatunk). Az osztály metódusaira @HandleBeforeCreate/HandleAfterCreate/HandleBeforeDelete/HandleAfterDelete/HandleAfterSave/HandleBeforeSave-t tehetünk. Az osztályt bean-ként kell létrehozni  
ref: [[1]](https://www.baeldung.com/spring-data-rest-events)  

## RepositoryRestController

  
min: osztály  
Olyan mint a RestController. Ennek segítségével az endpointjainkba tudunk PagedResourcesAssembler, és PersistentEntityResourceAssembler-t injektálni ami segít a válasz összebuildelésében  
  

## RepositoryRestResource

  
min: interfész (PagingAndSortingRepository/JpaRepository)  
fontosabb paraméterek: String path  
Összevonja DAO és Rest réteget. Olyan mint a JpaRepository csak a rest réteget is létrehozza hozzá. HATEOAS-t is alapból nyújt  
  

## RestResource

  
min: osztályra amin van @Repository/tagváltozó  
fontosabb paraméterek: String path, boolean exported  
Egy Repository-ból csinál HATEOAS képes endpointot. A RepositoryRestResource elődje, inkább azt használjuk. Ha tagváltozóra rakjuk akkor megadhatjuk vele, hogy az entitásba/dto-ba HATEOAS linket generáljon vagy az egész objektumot tegyük bele (exported)  
  

## SortDefault

  
min:   
fontosabb paraméterek: String name, Sort.Direction direction  
Page-nek alapértelmezett rendezést állíthatunk be  
  

Spring JMS
====
## ActiveMQAutoConfiguration

  
min: osztály  
Konfigurációs osztályra. Egy activeMQ broker-t hoz létre alapértelmezett beállításokkal  
  

## EnableJms

  
min: osztály  
JMS engedélyezése. Egy config osztáylra kell rakni, ami általában létrehoza a message driven configurációt (bean-eket: ConnectionFactory, JmsTemplate ))  
ref: [[1]](https://www.baeldung.com/spring-bean-vs-ejb)  

## JmsListener

  
min: metódus  
Consumer metódusra. Meghívódik, ha üzenet kerül a queue-ba. A metódus paramétere az üzenet, általában nincs visszatérési értéke. Üzenetet feladni a JmsTemplate.convertAndSend metódusán keresztül lehet  
ref: [[1]](https://www.baeldung.com/spring-bean-vs-ejb)  

## Service

  
min: osztály  
fontosabb paraméterek: String value  
Az osztály egy szervíz. A value paraméterrel megadhatjuk a spring bean nevét  
  

Spring Kafka
====
## EnableKafka

  
min: osztály (konfigurációs)  
Engedelyezi a kafka integrációt.  
ref: [[1]](https://www.baeldung.com/spring-kafka)  

## Header

  
min: metódus paraméter  
fontosabb paraméterek: String  
Ha több paramétere van egy @KafkaListener-nek, akkor megmondhatjuk vele, hogy melyikbe injektálja az üzenet fejlécet. A paraméter tipusa általában egy primitiv. Az értékével megmondhatjuk, hogy a fejléc melyik értékét injektáljuk. Ertekei a KafkaHeaders kostansai kuzul kerulnek ki  
ref: [[1]](https://www.baeldung.com/spring-kafka)[[2]](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/messaging/handler/annotation/Header.html)  

## KafkaListener

  
min: metódus  
fontosabb paraméterek: String topics, String groupId  
Esemény kezelő ami a topic-ban lévő üzenetre lefut. A metódus paramétere egy string, vagy egy object. Ha több paramétere van akkor fel kell annotálni öket @Payload-dal, és @Header-el  
ref: [[1]](https://www.baeldung.com/spring-kafka)  

## Payload

  
min: metódus paraméter  
Ha több paramétere van egy @KafkaListener-nek, akkor megmondhatjuk vele, hogy melyikbe injektálja az üzenet törzsét  
ref: [[1]](https://www.baeldung.com/spring-kafka)  

## SendTo

  
min: metódus  
fontosabb paraméterek: String  
A metódus visszatérési értékét konvertálja Message-é és broadcastolja a megadott topikba  
  

Spring Mongo integration
====
## DBRef

  
min: tagváltozó  
Lényegében egy join-t tudunk vele csinálni. Egy {"$ref" : "", "$id" : ""} formátumú struktúrát fog lementeni a subdocument-nek  
ref: [[1]](https://spring.io/blog/2021/11/29/spring-data-mongodb-relation-modelling)  

## EnableMongoRepositories

  
min: osztály  
Mongo Spring Data repository-k engedélyzése  
  

## org.springframework.data.mongodb.core.mapping.Document

  
min: osztály  
fontosabb paraméterek: String  
egy dokumentum típust definiál. A paraméter a collection neve  
  

## org.springframework.data.mongodb.core.mapping.MongoId

  
min: metódus/tagváltozó  
fontosabb paraméterek: FieldType  
A field az id. Definálhatunk neki típust  
  

## org.springframework.data.mongodb.repository.Query

  
min: interfész metódus definíció  
fontosabb paraméterek: String  
egy lekérdezés. A paramétere egy mongo query. Egy CrudRepository metódusára kell tenni  
  

## TypeAlias

  
min: osztály  
fontosabb paraméterek: String  
Typealias-t tudunk megadni az osztálynak. Ezzel elérhetjük, hogy az osztály teljes neve helyett ezzel azonosítsuk (pl. join-nál(DBRef))  
  

Spring Retry
====
## EnableRetry

  
min: osztály  
Spring retry engedélyezése  
ref: [[1]](https://github.com/spring-projects/spring-retry)  

Spring Security
====
## EnableAuthorizationServer

  
min: osztály (AuthServerOAuth2Config leszármazott)  
Oauth2 authentikációs szerver konfigurációs osztálya  
  

## EnableGlobalMethodSecurity

  
min: osztály (WebSecurityConfigurerAdapter)  
fontosabb paraméterek: boolean securedEnabled, boolean prePostEnabled, boolean jsr250Enabled  
Engedéylezhetjük vele a metódus szintű security check-et (@Secured, @Pre, @Post). A jsr250Enabled-el a standard javaee annotációkat tudjuk engedélyezni (RolesAllowed, PermitAll, DenyAll). A securedEnabled vagy jsr250Enabled közül valamelyiknek igaznak kell lennie.  
ref: [[1]](https://docs.spring.io/spring-security/site/docs/4.2.14.BUILD-SNAPSHOT/reference/htmlsingle/#enableglobalmethodsecurity)  

## EnableOAuth2Client

  
min: osztály  
Engedélyezi az oath2 authentikációt amikor az alkalmazásunk (mint kliens) kommuniál más alkalmazásokkal. Ezzel csinálhatunk OAuth2RestTemplate-et amit kliensként tudunk használni  
  

## EnableResourceServer

  
min: osztály  
Automatikusan ellenőrizni fogja az OAuth2 tokeneket a kérésekben (hozzáadja a security filtert a filterchain-hez). Kell egy ResourceServerConfigurerAdapter Beant létrehozni az alkalmazásban amin keresztül felkonfigurálhatjuk az oauth szerver elérhetőségét, és egyéb paramétereit, valamint az EnableWebSecurity annotációt is fel kell valahova rakni  
ref: [[1]](https://docs.spring.io/spring-security/oauth/apidocs/org/springframework/security/oauth2/config/annotation/web/configuration/EnableResourceServer.html)  

## EnableWebSecurity

  
min: osztály  
Az osztály elindítja a webes security-t amivel konfigurálni lehet a webes endpointokat (WebSecurityConfigurerAdapter-t ki kell dolgozni ehhez)  
  

## PostAuthorize

  
min: metódus  
fontosabb paraméterek: String  
Egy authentikációs kifejezést adhatunk meg, ami lefut miután végrehajtjuk a metódust.  
  

## PostFilter

  
min: metódus  
fontosabb paraméterek: String  
Megadhatunk egy filterezési paramétert a metódus (Collection tipusú) visszatérési értékére. Pl. "filterObject != authentication.principal.username"  
  

## PreAuthorize

  
min: metódus  
fontosabb paraméterek: String  
Egy authentikációs kifejezést adhatunk meg, ami lefut mielött végrehajtjuk a metódust. Pl. egy kifejezésre: "hasRole('ROLE_VIEWER')"  
  

## PreFilter

  
min: metódus  
fontosabb paraméterek: String filterTarget, String value  
Megadhatunk egy filterezési (authentikációs) kifejezést Collection típusú metódus paraméterekre. A paraméter neve a filterTarget  
  

## Secured

  
min: osztály/metódus  
fontosabb paraméterek: String[]  
Olyan mint a RolesAllowed, bár azt is használhatjuk. Megadhatjuk, hogy milyen ROLE-lal (kell a "ROLE" prefix) rendelkező felhasználók futtathatják a metódust. Hatását a WebSecurityConfig-nál kell egy @EnableGlobalMethodSecurity(securedEnabled = true)-al bekapcsolni  
  

Spring WS
====
## EnableWs

  
min: osztály  
konfigurációs osztályon jelezhetjük, hogy az alkalmazásunk webservice-eket (@Endpoint) kínál  
  

## Endpoint

  
min: osztály  
fontosabb paraméterek: String  
Az osztály webservice funkciókat valósít meg. A paraméter egy logikai komponenst jelent  
ref: [[1]](https://docs.spring.io/spring-ws/site/apidocs/org/springframework/ws/server/endpoint/annotation/Endpoint.html)  

## PayloadRoot

  
min: metódus  
fontosabb paraméterek: String localPart, String namespace  
Egy Webservice metódus. A localPart jelöli ki, hogy milyen funciót hívunk, ennek az értéke általában a metódus paraméterének típusa (string-ként). Ajánlott azt megadni, mert lehet, hogy nem fogja mappelni az üzenetet az endpointra  
  

## RequestPayload

  
min: metódus paraméter  
A Webservice metódus egy Soap üzenetet vár  
  

## ResponsePayload

  
min: metódus  
A Webservice metódus egy Soap üzenettel tér vissza  
  

## SoapAction

  
min: metódus  
fontosabb paraméterek: String  
Ha a kérésben a SOAPAction header ki van töltve (a megadott értékkel) akkor ezt a metódust fogja végrehajtani  
ref: [[1]](https://docs.spring.io/spring-ws/sites/1.5/apidocs/org/springframework/ws/soap/server/endpoint/annotation/SoapAction.html)  

## SoapFault

  
min: osztály (Exception)  
fontosabb paraméterek: FaultCode faultCode  
Megadhatjuk, hogy ha a webservice metódusunk ezt a kivételt dobja akkor milyen fault kóddal térjünk vissza  
ref: [[1]](https://docs.spring.io/spring-ws/sites/1.5/reference/html/server.html)  

## XPathParam

  
min: metódus paraméter  
fontosabb paraméterek: String  
path paramétert adhatunk meg vele. Pl: @XPathParam("/s:orderRequest/@id") double orderId  
ref: [[1]](https://docs.spring.io/spring-ws/sites/1.5/reference/html/server.html#server-automatic-wsdl-exposure)  

Spring Web
====
## AutoConfigureWebClient

  
min: osztály  
Webkliensek auto konfigurálása  
  

## AutoConfigureWebMvc

  
min: osztály  
Teszt osztályra szokás rakni. Konfigurálja a webréteghez tartozó dolgokat  
  

## Controller

  
min: osztály  
fontosabb paraméterek: String value  
Az osztály megfelel az MVC pattern Controllerének. A value paraméterrel megadhatjuk a spring bean nevét  
  

## ControllerAdvice

  
min: osztály  
Az osztály ExceptionHandler-eket definiál.  
  

## CookieValue

  
min: metódus paraméter  
fontosabb paraméterek: String name, String defaultValue  
A paramétert a sütiből veszi  
  

## CrossOrigin

  
min: osztály/metódus  
fontosabb paraméterek: String[] origins, String[] allowedHeaders  
Cors headert állíthatunk be a RepositoryRestResource-unknak. Alapból mindent engedélyezni fog (*). Csak akkor használjuk, ha egy-egy RestController-nek külön cors header kell. A fejlesztéshez a localhost engedélyezését inkább globális konfigurációból oldjuk meg  
  

## DateTimeFormat

  
min: metódus/tagváltozó/paraméter  
fontosabb paraméterek: DateTimeFormat.ISO, String pattern  
Megadhatjuk, hogy a LocalDate-et milyen formátumra/ról konvertálja  
  

## DeleteMapping

  
min: metódus  
fontosabb paraméterek: String  
Delete. Érdemes void helyett legalább egy ResponseEntity objektumot megadni, különben a Spring (sikeres végrehajtás után is) dobhat egy 404-et. Body-t nem ajánlott megadni, mert a swagger codegen javascript kliens generálásnál hibát dobhat.  
  

## EnableWebMvc

  
min: osztály  
Engedélyezi az MVC-t a WebMvcConfigurationSupport-ban lévő konfiguráció szerint. Vigyázni vele, mert lehet, hogy felűlcsapja a saját konfigurációnkat  
ref: [[1]](https://stackoverflow.com/questions/50177432/spring-webmvcconfigurer-running-twice)  

## EnableWebSocket

  
min: osztály (@Configuration)  
WebSocketet engedélyezi. Általában  WebSocketMessageBrokerConfigurer-t implementalo osztályra szokás tenni  
ref: [[1]](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/web/socket/config/annotation/EnableWebSocket.html)[[2]](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/web/socket/config/annotation/EnableWebSocket.html)  

## EnableWebSocketMessageBroker

  
min: osztály (@Configuration)  
Engedélyezi a a messageBrokert. Általában WebSocketMessageBrokerConfigurer-t implementalo osztályra szokás tenni  
  

## ExceptionHandler

  
min: metódus  
fontosabb paraméterek: Class<? extends Throwable>[]  
A metódus egy ExceptionHandler. A ExceptionMapper Springes megfelelője Visszatérési értéke egy ResponseEntity (vagy vagy ModelAndView), paramétere egy Exception (amit el kap), és egy WebRequest. Az osztályra egy @ControllerAdvice kell.  
  

## JsonComponent

  
min: osztály  
Jelzi, hogy az osztálynak vannak olyan belső osztályai amikkel JSON-t lehet parsolni (JsonSerializer,JsonDeserializer)  
  

## MessageMapping

  
min: metódus  
fontosabb paraméterek: String  
MessageHandler a metódus  
  

## ModelAttribute

  
min: metódus paraméter  
Thymeleaf-fel használt oldalon ha egy form-ot submit-olunk akkor a form inputjainak csinálhatunk egy befoglaló osztályt. Ez az osztály lesz a metódus bemenő paramétere, erre kell rakni ezt az annotációt. A metódusra meg a standard @RequestMapping-ot. Akkor is használhatjuk ha amúgy egy request feldolgozó metódusnak Map<String, String> paramétert adnánk. Ezzel validációt is hozzáadhatunk  
ref: [[1]](https://www.baeldung.com/sprint-boot-multipart-requests)  

## PathVariable

  
min: metódus  
fontosabb paraméterek: String  
PathParam Springes megfelelője  
  

## RequestAttribute

  
min: metódus paraméter  
fontosabb paraméterek: String  
Request attribútumát lemappeli egy paraméterre  
  

## RequestBody

  
min: metódus paraméter  
A request body-ját konvertálja objektummá. JavaEE-nél ez automatikusan megy (form-url encodednál ne használjuk)  
  

## RequestMapping

  
min: osztály/metódus  
fontosabb paraméterek: String[] value, method, consumes, produces  
HTTP endpontokat hozhatunk létre vele. (A path tulajdonságot nem fogja lemappelni a swagger, használjuk a value-t)  
  

## RequestParam

  
min: metódus paraméter  
fontosabb paraméterek: String value, defaultValue  
QueryParam Springes megfelelője. Tudunk vele MultipartFile-t injektálni a fájlfeltöltéshez. Ilyenkor a String paraméter a file input neve  
  

## ResponseBody

  
min: osztály/metódus  
A függvény visszatérési értékét parsoljuk, response-zá. Endpointokra szokás rakni. Jelzi, hogy a visszatérési érték mondjuk nem egy html fájlra redirectel.  
  

## ResponseStatus

  
min: osztály/metódus  
fontosabb paraméterek: int  
Mi legyen a válasz státuszkódja. Saját Exception típusra kell rakni, ezzel alapértelmezett státuszkódot tudunk hozzá társítani.  
  

## RestController

  
min: osztály  
fontosabb paraméterek: String  
Ekvivalens a Controller és ResponesBody annotáció párossal. Az osztály RequestMapping metódusokat tartalmaz. A paraméter csak egy logikai név, az url előállításában nincs szerepe. (Nevének megfelelően ajánlott, ha a metódusai követik a REST előírásait)  
ref: [[1]](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/web/bind/annotation/RestController.html)  

## ServletComponentScan

  
min: osztály  
fontosabb paraméterek: String[] basePackages, Class<?>[] basePackageClasses  
Embedded web server módban automatikusan felismeri a WebServlet, WebFilter, WebListener-eket. Szabályozható, hogy csak bizonyos csomagokon futtassa detektálást.  
ref: [[1]](https://docs.spring.io/spring-boot/docs/current/api/org/springframework/boot/web/servlet/ServletComponentScan.html)  

## Validated

  
min: metódus/osztály/paraméter  
A @Valid annotáció springes megfelelője. Az ezzel annotált osztályok/objektumok alobjektumaira is elvégzi a validációt  
ref: [[1]](https://docs.spring.io/spring/docs/current/javadoc-api/org/springframework/validation/annotation/Validated.html)  

Spring Web Test
====
## AutoConfigureMockMvc

  
min: osztály  
A teszt osztályra kell tenni. A MockMvc-hez tartozó dolgokat konfigurálja. Tudunk vele MockMvc-t injektálni  
  

## RestClientTest

  
min: osztály  
RestTemplate tesztelésére szolgáló annotáció  
ref: [[1]](https://rieckpil.de/testing-your-spring-resttemplate-with-restclienttest/)  

## WebMvcTest

  
min: osztály  
fontosabb paraméterek: Class[]  
Csak a web réteget tölti be, azt tudjuk tesztelni. Meg tudjuk adni, hogy mely controllereket töltsük még be vele együtt  
  

Spring WebFlux
====
## EnableReactiveMethodSecurity

  
min: osztály (@Configuration)  
Metódus szinten határozhatjuk meg a Security-t vele. (A EnableWebFluxSecurity ellentétben, ami apath szinten megy)  
ref: [[1]](https://dzone.com/articles/webflux-reactive-programming-with-spring-part-3)  

## EnableWebFluxSecurity

  
min: osztály (@Configuration)  
Engedélyezzük vele a WebFlux Security-t  
ref: [[1]](https://dzone.com/articles/webflux-reactive-programming-with-spring-part-3)  


