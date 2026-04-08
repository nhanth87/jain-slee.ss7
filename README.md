# 🚀 jain-slee.ss7-NG 9.2.3 - JAIN SLEE SS7 Resource Adaptors

> **JAIN SLEE Integration | jSS7-NG Powered | High-Performance RA**

[![jain-slee.ss7-NG](https://img.shields.io/badge/jain--slee.ss7--NG-9.2.3-blue.svg)](https://github.com/nhanth87/jain-slee.ss7)
[![jSS7](https://img.shields.io/badge/Powered%20by-jSS7--NG%209.2.4-orange.svg)](https://github.com/nhanth87/jSS7)
[![JAIN SLEE](https://img.shields.io/badge/JAIN%20SLEE-1.1-green.svg)](https://jcp.org/en/jsr/detail?id=240)

---

## 💡 Overview

**jain-slee.ss7-NG** provides JAIN SLEE Resource Adaptors (RA) for SS7 protocols, integrating the high-performance **jSS7-NG 9.2.4** stack into the JAIN SLEE ecosystem.

### Resource Adaptors Included

| RA | Protocol | Use Case |
|----|----------|----------|
| **MAP-RA** | Mobile Application Part | Subscriber management, SMS, location |
| **CAP-RA** | CAMEL Application Part | IN services, prepaid, call control |
| **TCAP-RA** | Transaction Capabilities | Dialog management, operations |
| **ISUP-RA** | ISDN User Part | Call setup, voice circuits |

---

## 🎯 Key Features

### 1. JAIN SLEE 1.1 Compliant
- Full SLEE specification compliance
- Standard activity management
- Event routing and transaction support

### 2. jSS7-NG Integration
```xml
<!-- Dependencies -->
<jSS7.version>9.2.4</jSS7.version>
<sctp.version>2.0.8</sctp.version>

<!-- Benefits -->
- JCTools collections (lock-free)
- XStream serialization
- Zero-GC SCTP transport
```

### 3. High-Performance RA Design
```java
// RA uses jSS7-NG's optimized components
@ResourceAdaptorType
public class MapResourceAdaptor {
    // NonBlockingHashMap for subscriber cache
    // MpscArrayQueue for event buffering
    // Zero-copy message handling
}
```

---

## 📊 Architecture

```
┌─────────────────────────────────────────────┐
│         JAIN SLEE Container                  │
│  ┌─────────────────────────────────────┐    │
│  │         SBB Application              │    │
│  │   (Your Telecom Service Logic)       │    │
│  └─────────────────────────────────────┘    │
│              │                               │
│  ┌───────────┼───────────┐                   │
│  │           │           │                   │
│  ▼           ▼           ▼                   │
│ MAP-RA    CAP-RA    TCAP-RA                  │
│  │           │           │                   │
│  └───────────┴───────────┘                   │
│              │                               │
│  ┌───────────▼───────────┐                   │
│  │     jSS7-NG 9.2.4      │                   │
│  │  (JCTools + XStream)   │                   │
│  └────────────────────────┘                   │
│              │                               │
│  ┌───────────▼───────────┐                   │
│  │     SCTP-NG 2.0.8      │                   │
│  │   (Zero-GC Transport)  │                   │
│  └────────────────────────┘                   │
└─────────────────────────────────────────────┘
```

---

## 🛠️ Building

### Prerequisites
- Java 11
- Maven 3.6+
- JAIN SLEE 1.1 container (WildFly/Restcomm)

### Maven Build
```bash
mvn clean install -DskipTests -Dcheckstyle.skip=true
```

### Output
- `restcomm-slee-ra-map-du-*.jar`
- `restcomm-slee-ra-cap-du-*.jar`
- `restcomm-slee-ra-tcap-du-*.jar`
- `restcomm-slee-ra-isup-du-*.jar`

---

## 📦 Deployment

### 1. Build Deployable Units (DU)
```bash
cd resources/map/du
mvn clean package
```

### 2. Deploy to SLEE Container
```bash
# Copy DU to SLEE deploy directory
cp target/restcomm-slee-ra-map-du-*.jar $JBOSS_HOME/standalone/deployments/
```

### 3. Configure RA Entity
```xml
<resource-adaptor-entity>
    <name>MapRA</name>
    <resource-adaptor-type-name>
        ResourceAdaptorTypeMap
    </resource-adaptor-type-name>
</resource-adaptor-entity>
```

---

## 🔧 Configuration

### RA Properties
```properties
# MAP RA
MAP_JNDI=java:/restcomm/ss7/map
SCCP_JNDI=java:/restcomm/ss7/sccp

# CAP RA  
CAP_JNDI=java:/restcomm/ss7/cap
TCAP_JNDI=java:/restcomm/ss7/tcap
```

### jSS7-NG Integration
```xml
<dependency>
    <groupId>org.restcomm.protocols.ss7</groupId>
    <artifactId>map-ra</artifactId>
    <version>9.2.4</version>
</dependency>
```

---

## 📝 Changelog

### v9.2.3 (Current)
- ✅ Updated: jSS7-NG 9.2.4 dependency
- ✅ Updated: SCTP-NG 2.0.8 for zero-GC transport

### v9.2.2
- ✅ Updated: jSS7 9.2.3 compatibility

### v9.2.1
- ✅ Updated: jSS7-NG 9.2.1 with JCTools migration

---

## 📄 License

GNU Lesser General Public License v2.1

---

**Maintained by:** nhanth87  
**Powered by:** jSS7-NG 9.2.4 | JAIN SLEE 1.1  
**For:** High-performance telecom services
